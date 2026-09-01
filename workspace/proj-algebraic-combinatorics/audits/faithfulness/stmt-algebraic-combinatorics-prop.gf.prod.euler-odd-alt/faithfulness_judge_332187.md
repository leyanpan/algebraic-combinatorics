## TARGET euler_odd_parts_identity' (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] [inst_1 : TopologicalSpace K] [IsTopologicalRing K] [T2Space K] [NoZeroDivisors K],
  ∏' (i : { n // Odd ↑n }), Ring.inverse (1 - PowerSeries.X ^ ↑↑i) = ∏' (k : ℕ+), (1 + PowerSeries.X ^ ↑k)

Docstring: Alternative form of Euler's identity using the set of odd positive integers.

This follows from `euler_odd_parts_identity` by reindexing the product using the
equivalence `oddPNatEquivPNat` between `{ n : ℕ+ // Odd n }` and `ℕ+`. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF TopologicalSpace
Type u → Type u

Docstring: A topology on `X`. 

## BASE-LIBRARY REF IsTopologicalRing
(R : Type u_1) → [TopologicalSpace R] → [NonUnitalNonAssocRing R] → Prop

Docstring: A topological ring is a ring `R` where addition, multiplication and negation are continuous.

If `R` is a (unital) ring, then continuity of negation can be derived from continuity of
multiplication as it is multiplication with `-1`. (See
`IsTopologicalSemiring.continuousNeg_of_mul` and
`topological_semiring.to_topological_add_group`) 

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF T2Space
(X : Type u) → [TopologicalSpace X] → Prop

Docstring: A T₂ space, also known as a Hausdorff space, is one in which for every
`x ≠ y` there exists disjoint open sets around `x` and `y`. This is
the most widely used of the separation axioms. 

## BASE-LIBRARY REF NoZeroDivisors
(M₀ : Type u_2) → [Mul M₀] → [Zero M₀] → Prop

Docstring: Predicate typeclass for expressing that `a * b = 0` implies `a = 0` or `b = 0`
for all `a` and `b` of type `M₀`. It is weaker than `IsCancelMulZero` in general,
but equivalent to it if `M₀` is a (not necessarily unital or associative) ring. 

## BASE-LIBRARY REF Distrib.toMul
{R : Type u_1} → [self : Distrib R] → Mul R

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toDistrib
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → Distrib α

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toMulZeroClass
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → MulZeroClass α

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

## BASE-LIBRARY REF Subtype
{α : Sort u} → (α → Prop) → Sort (max 1 u)

Docstring: All the elements of a type that satisfy a predicate.

`Subtype p`, usually written `{ x : α // p x }` or `{ x // p x }`, contains all elements `x : α` for
which `p x` is true. Its constructor is a pair of the value and the proof that it satisfies the
predicate. In run-time code, `{ x : α // p x }` is represented identically to `α`.

There is a coercion from `{ x : α // p x }` to `α`, so elements of a subtype may be used where the
underlying type is expected.

Examples:
 * `{ n : Nat // n % 2 = 0 }` is the type of even numbers.
 * `{ xs : Array String // xs.size = 5 }` is the type of arrays with five `String`s.
 * Given `xs : List α`, `List { x : α // x ∈ xs }` is the type of lists in which all elements are
   contained in `xs`.


Conventions for notations in identifiers:

 * The recommended spelling of `{ x // p x }` in identifiers is `subtype`.

## BASE-LIBRARY REF PNat
Type

Docstring: `ℕ+` is the type of positive natural numbers. It is defined as a subtype,
and the VM representation of `ℕ+` is the same as `ℕ` because the proof
is not stored. 

## BASE-LIBRARY REF Odd
{α : Type u_2} → [Semiring α] → α → Prop

Docstring: An element `a` of a semiring is odd if there exists `k` such `a = 2*k + 1`. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Nat.instSemiring
Semiring ℕ

## BASE-LIBRARY REF PNat.val
ℕ+ → ℕ

Docstring: The underlying natural number 

## BASE-LIBRARY REF CommRing.toCommMonoid
{α : Type u} → [self : CommRing α] → CommMonoid α

## BASE-LIBRARY REF PowerSeries.instCommRing
{R : Type u_1} → [CommRing R] → CommRing (PowerSeries R)

## BASE-LIBRARY REF PowerSeries.WithPiTopology.instTopologicalSpace
(R : Type u_1) → [TopologicalSpace R] → TopologicalSpace (PowerSeries R)

Docstring: The pointwise topology on `PowerSeries` 

## BASE-LIBRARY REF Ring.inverse
{M₀ : Type u_2} → [MonoidWithZero M₀] → M₀ → M₀

Docstring: Introduce a function `inverse` on a monoid with zero `M₀`, which sends `x` to `x⁻¹` if `x` is
invertible and to `0` otherwise.  This definition is somewhat ad hoc, but one needs a fully (rather
than partially) defined inverse function for some purposes, including for calculus.

Note that while this is in the `Ring` namespace for brevity, it requires the weaker assumption
`MonoidWithZero M₀` instead of `Ring M₀`. 

## BASE-LIBRARY REF Semiring.toMonoidWithZero
{α : Type u} → [self : Semiring α] → MonoidWithZero α

## BASE-LIBRARY REF PowerSeries.instSemiring
{R : Type u_1} → [Semiring R] → Semiring (PowerSeries R)

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

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

## BASE-LIBRARY REF Unit
Type

Docstring: The canonical type with one element. This element is written `()`.

`Unit` has a number of uses:
* It can be used to model control flow that returns from a function call without providing other
  information.
* Monadic actions that return `Unit` have side effects without computing values.
* In polymorphic types, it can be used to indicate that no data is to be stored in a particular
  field.


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

## BASE-LIBRARY REF PowerSeries.X
{R : Type u_1} → [Semiring R] → PowerSeries R

Docstring: The variable of the formal power series ring. 

## BASE-LIBRARY REF Subtype.val
{α : Sort u} → {p : α → Prop} → Subtype p → α

Docstring: The value in the underlying type that satisfies the predicate.


## BASE-LIBRARY REF SummationFilter.unconditional
(β : Type u_2) → SummationFilter β

Docstring: **Unconditional summation**: a function on `β` is said to be *unconditionally summable* if its
partial sums over finite subsets converge with respect to the `atTop` filter. 

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

## INFORMAL STATEMENT
prop.gf.prod.euler-odd-alt

\leanhelper  Alternative formulation of Euler’s identity: indexing the left-hand side over odd positive integers rather than all positive integers, 

\[  \prod _{\substack {i\in \mathbb {N}^{+}\\ i\text{ odd}}} \left(1-x^i\right)^{-1} = \prod _{k>0}\left(1+x^k\right).  \]

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.lim.ismultipliable
def.fps.lim.isMultipliable

\leanhelper  A family $(f_n)_{n \in \mathbb {N}}$ of FPSs is \emph{multipliable} if (1) $[x^0]f_i = 1$ for all $i$, and (2) for each $n \in \mathbb {N}$, there exists $N$ such that for all $i \geq N$ and all $k \leq n$, $[x^k]f_i = \delta _{k,0}$ (i.e., eventually all $f_i$ are $\equiv 1 \pmod{x^{n+1}}$).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.lim.tprod
def.fps.lim.tprod

\leanhelper  The \emph{infinite product} of a multipliable family $(f_n)_{n \in \mathbb {N}}$ is the FPS $\prod _{n \in \mathbb {N}} f_n$ whose $n$-th coefficient equals $[x^n](\prod _{j=0}^{N} f_j)$ for any sufficiently large $N$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.xneq
def.fps.xneq

Let $n\in \mathbb {N}$. Let $f,g\in K\left[\left[x\right]\right]$ be two FPSs. We write $f\overset {x^{n}}{\equiv }g$ if and only if 

\[  \text{each }m\in \left\{ 0,1,\ldots ,n\right\} \text{ satisfies } \left[x^{m}\right]f=\left[x^{m}\right]g.  \]

Thus, we have defined a binary relation $\overset {x^{n}}{\equiv }$ on the set $K\left[\left[x\right]\right]$. We say that an FPS $f$ is $x^{n}$\emph{-equivalent} to an FPS $g$ if and only if $f\overset {x^{n}}{\equiv }g$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal equality matches the blueprint term-for-term: `\u220f' (i : { n // Odd \u2191n }), Ring.inverse (1 - PowerSeries.X ^ \u2191\u2191i)` indexes the left side by odd elements of `\u2115+`, while `\u220f' (k : \u2115+), (1 + PowerSeries.X ^ \u2191k)` indexes the right side by all positive integers. `PowerSeries.X` is the formal variable, and `Ring.inverse` is the total inverse; here each `1 - X^i` is invertible as a formal power series, so it represents the blueprint\u2019s `(1-x^i)\u207b\u00b9`. The binders `[TopologicalSpace K] [IsTopologicalRing K] [T2Space K]` encode the setting required by the library\u2019s topology-based `tprod`; for these coefficientwise-stabilizing products this serves as the formal implementation of the blueprint\u2019s infinite product rather than changing its mathematical content. The blueprint\u2019s geometric-series definition assumes `K` is a field, whereas the target only requires `[CommRing K] [NoZeroDivisors K]`; this is algebraically more general, not weaker than the blueprint. Every field satisfies those algebraic assumptions, and a suitable topology (for example, the discrete topology) supplies the encoding instances."
}