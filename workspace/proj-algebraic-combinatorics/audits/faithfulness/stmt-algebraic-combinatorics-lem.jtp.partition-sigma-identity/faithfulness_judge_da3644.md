## TARGET AlgebraicCombinatorics.partition_sigma_identity (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ),
  ↑n * ↑(AlgebraicCombinatorics.partitionCount n) =
    ∑ p ∈ Finset.antidiagonal n with p.1 ≠ 0,
      ↑((ArithmeticFunction.sigma 1) p.1) * ↑(AlgebraicCombinatorics.partitionCount p.2)

Docstring: **Key Combinatorial Identity**: n * p(n) = ∑_{k=1}^n σ_1(k) * p(n-k)

This identity relates the partition function p(n) to the sum of divisors function σ_1.

## Proof Approaches

### 1. Logarithmic Derivative (Classical)
Since P = ∏_{k≥1} 1/(1-X^k), we have:
- log(P) = -∑_{k≥1} log(1-X^k) = ∑_{k≥1} ∑_{m≥1} X^{km}/m
- X * d/dX log(P) = ∑_{k≥1} ∑_{m≥1} k * X^{km} = ∑_{n≥1} σ_1(n) * X^n = S
- Since d/dX log(P) = P'/P, we get X * P'/P = S, hence X * P' = S * P.

This approach requires PowerSeries.log which is not yet in Mathlib.

### 2. Combinatorial Bijection
The identity can be proved by establishing a bijection between:
- **Type A**: Pairs (λ, cell) where λ partitions n and cell ∈ {1,...,n} marks a cell in the Young diagram
- **Type B**: Quadruples (d, m, j, μ) where:
  - d ≥ 1 is a part size
  - m ≥ 1 is a multiplicity (so md ≤ n)
  - j ∈ {1,...,d} is a position within a row
  - μ partitions n - md

The bijection:
- **Forward**: (λ, cell) → (d, m, j, μ) where d = length of row containing cell,
  m = count of d-rows in λ, j = position of cell in its row, μ = λ minus all d-rows
- **Backward**: (d, m, j, μ) → (λ, cell) where λ = μ plus m rows of length d,
  cell = position j in the first new row

Counting:
- |Type A| = n * p(n) (n cells per partition, p(n) partitions)
- |Type B| = ∑_{d,m: md≤n} d * p(n-md) = ∑_{k=1}^n (∑_{d|k} d) * p(n-k) = ∑_{k=1}^n σ_1(k) * p(n-k)

### 3. Direct Verification
One can verify the identity directly by computing both sides for each n,
using the recursive formula for p(n) from Euler's pentagonal theorem.

## Note
This lemma is the key remaining piece for proving `euler_sum_divisors_recursive`.
The bijection approach is the most elementary but requires formalizing Young diagrams
and cell positions. The logarithmic derivative approach is cleaner but requires
infrastructure for power series logarithms.


## PROJECT DEPENDENCY AlgebraicCombinatorics.partitionCount (def)
ℕ → ℕ

Body:
Nat.Partition.partitionCount

Docstring: Local alias for `Nat.Partition.partitionCount` from `Partitions/Basics.lean`.
This provides compatibility with existing code in this file. 

## PROJECT DEPENDENCY Nat.Partition.partitionCount (def)
ℕ → ℕ

Body:
fun n => Fintype.card n.Partition

Docstring: The partition function `p(n)`: the number of partitions of `n`.
(Definition \ref{def.pars.pn-pkn} (b)) 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


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

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


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


## BASE-LIBRARY REF instNatCastInt
NatCast ℤ

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF Int.instAddCommMonoid
AddCommMonoid ℤ

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF instDecidableNot
{p : Prop} → [dp : Decidable p] → Decidable ¬p

## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF Finset.HasAntidiagonal.antidiagonal
{A : Type u_1} → {inst : AddMonoid A} → [self : Finset.HasAntidiagonal A] → A → Finset (A × A)

Docstring: The antidiagonal of an element `n` is the finset of pairs `(i, j)` such that `i + j = n`. 

## BASE-LIBRARY REF Nat.instAddMonoid
AddMonoid ℕ

## BASE-LIBRARY REF Finset.Nat.instHasAntidiagonal
Finset.HasAntidiagonal ℕ

Docstring: The antidiagonal of a natural number `n` is
the finset of pairs `(i, j)` such that `i + j = n`. 

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF ArithmeticFunction
(R : Type u_1) → [Zero R] → Type (max 0 u_1)

Docstring: An arithmetic function is a function from `ℕ` that maps 0 to 0. In the literature, they are
often instead defined as functions from `ℕ+`. Multiplication on `ArithmeticFunctions` is by
Dirichlet convolution. 

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

## BASE-LIBRARY REF ArithmeticFunction.instFunLikeNat
{R : Type u_1} → [inst : Zero R] → FunLike (ArithmeticFunction R) ℕ R

## BASE-LIBRARY REF ArithmeticFunction.sigma
ℕ → ArithmeticFunction ℕ

Docstring: `σ k n` is the sum of the `k`th powers of the divisors of `n` 

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

## BASE-LIBRARY REF Fintype.card
(α : Type u_4) → [Fintype α] → ℕ

Docstring: `card α` is the number of elements in `α`, defined when `α` is a fintype. 

## BASE-LIBRARY REF Nat.Partition
ℕ → Type

Docstring: A partition of `n` is a multiset of positive integers summing to `n`. 

## BASE-LIBRARY REF Nat.Partition.instFintype
(n : ℕ) → Fintype n.Partition

Docstring: Show there are finitely many partitions by considering the surjection from compositions to
partitions.


## INFORMAL STATEMENT
lem.jtp.partition-sigma-identity

\leanhelper  For each $n\in \mathbb {N}$, 

\[  n\cdot p(n) = \sum _{k=1}^{n} \sigma (k)\cdot p(n-k).  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.comps
def.fps.comps

\textbf{(a)} An \emph{(integer) composition} means a (finite) tuple of positive integers. \medskip 

\textbf{(b)} The \emph{size} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $\alpha _{1}+\alpha _{2}+\cdots +\alpha _{m}$. It is written $\left\vert \alpha \right\vert $. \medskip 

\textbf{(c)} The \emph{length} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $m$. It is written $\ell \left( \alpha \right) $. \medskip 

\textbf{(d)} Let $n\in \mathbb {N}$. A \emph{composition of }$n$ means a composition whose size is $n$. \medskip 

\textbf{(e)} Let $n\in \mathbb {N}$ and $k\in \mathbb {N}$. A \emph{composition of }$n$\emph{ into }$k$\emph{ parts} is a composition whose size is $n$ and whose length is $k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.jtp.sigmaseries
def.jtp.sigmaSeries

\leanhelper  The \emph{sum-of-divisors generating function} is 

\[  S = \sum _{k>0} \sigma (k)\,  x^k \in \mathbb {Z}[[x]],  \]

 where $\sigma (k) = \sigma _1(k) = \sum _{d\mid k} d$ is the sum of positive divisors of~ $k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pars.parts
def.pars.parts

\textbf{(a)} An \emph{(integer) partition} means a (finite) weakly decreasing tuple of positive integers – i.e., a finite tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{m}\right) $ of positive integers such that $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{m}$. 

Thus, partitions are the same as weakly decreasing compositions. Hence, the notions of \emph{size} and \emph{length} of a partition are automatically defined, since we have defined them for compositions (in Definition \ref{def.fps.comps}). \medskip 

\textbf{(b)} The \emph{parts} of a partition $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{m}\right) $ are simply its entries $\lambda _{1},\lambda _{2},\ldots ,\lambda _{m}$. \medskip 

\textbf{(c)} Let $n\in \mathbb {Z}$. A \emph{partition of }$n$ means a partition whose size is $n$. \medskip 

\textbf{(d)} Let $n\in \mathbb {Z}$ and $k\in \mathbb {N}$. A \emph{partition of }$n$\emph{ into }$k$\emph{ parts} is a partition whose size is $n$ and whose length is $k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pars.pn-pkn
def.pars.pn-pkn

\textbf{(a)} Let $n\in \mathbb {Z}$ and $k\in \mathbb {N}$. Then, we set

\[  p_{k}\left( n\right) :=\left( \text{\#  of partitions of }n\text{ into }k\text{ parts}\right) .  \]

\textbf{(b)} Let $n\in \mathbb {Z}$. Then, we set

\[  p\left( n\right) :=\left( \text{\#  of partitions of }n\right) .  \]

 This is called the $n$\emph{-th partition number}.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target quantifies exactly as required: `\u2200 (n : \u2115)`. Its left side `\u2191n * \u2191(AlgebraicCombinatorics.partitionCount n)` is the integer-valued form of `n \u00b7 p(n)`, since `partitionCount n` has body `Fintype.card n.Partition`, and `Nat.Partition` is documented as the type of partitions of `n`. On the right, `Finset.antidiagonal n` consists of pairs `(k,j)` with `k + j = n`; filtering by `p.1 \u2260 0` makes `k` range from `1` through `n`, with `j = n-k`. Thus `\u2211 p \u2208 Finset.antidiagonal n with p.1 \u2260 0, \u2191((ArithmeticFunction.sigma 1) p.1) * \u2191(partitionCount p.2)` is exactly `\u2211_{k=1}^n \u03c3\u2081(k) p(n-k)`. The library docstring states that `ArithmeticFunction.sigma 1` sums first powers of divisors, matching the informal definition `\u03c3(k)=\u03c3\u2081(k)=\u2211_{d\u2223k} d`. Casting both sides to `\u2124` changes only the ambient type of the equality, not its mathematical content."
}