## TARGET Nat.Partition.coeff_P (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ), (PowerSeries.coeff n) Nat.Partition.P = ↑(Nat.Partition.partitionCount n)

Docstring: The coefficient of x^n in P equals p(n). 

## PROJECT DEPENDENCY Nat.Partition.P (def)
PowerSeries ℤ

Body:
Nat.Partition.genFun fun x x_1 => 1

Docstring: The partition generating function P = ∑_{n≥0} p(n) x^n, specialized to ℤ coefficients. 

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


## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

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

## BASE-LIBRARY REF Int.instSemiring
Semiring ℤ

## BASE-LIBRARY REF RingHom.id
(α : Type u_5) → [inst : NonAssocSemiring α] → α →+* α

Docstring: The identity ring homomorphism from a semiring to itself. 

## BASE-LIBRARY REF Semiring.toNonAssocSemiring
{α : Type u} → [self : Semiring α] → NonAssocSemiring α

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF PowerSeries.instAddCommMonoid
{R : Type u_1} → [AddCommMonoid R] → AddCommMonoid (PowerSeries R)

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toAddCommMonoid
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → AddCommMonoid α

## BASE-LIBRARY REF NonAssocSemiring.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonAssocSemiring α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF PowerSeries.instModule
{R : Type u_1} →
  {A : Type u_2} →
    [inst : Semiring R] → [inst_1 : AddCommMonoid A] → [_root_.Module R A] → _root_.Module R (PowerSeries A)

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

## BASE-LIBRARY REF Nat.Partition.genFun
{R : Type u_1} → [CommSemiring R] → (ℕ → ℕ → R) → PowerSeries R

Docstring: Generating function associated with character $f(i, c)$ for partition functions, where $i$ is a
part of the partition, and $c$ is the count of that part in the partition. The character function is
multiplied within one `n.Partition`, and summed among all `n.Partition` for a fixed `n`. This way,
each `n` is assigned a value, which we use as the coefficients of the power series.

See the module docstring of `Combinatorics.Enumerative.Partition.GenFun` for more details. 

## BASE-LIBRARY REF Int.instCommSemiring
CommSemiring ℤ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

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
lem.pars.coeff-P

\leanhelper  The coefficient of $x^n$ in $P$ equals $p(n)$: $[x^n]P = p(n)$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.coeff
def.fps.coeff

If $n\in \mathbb {N}$, and if $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right) \in K\left[\left[x\right]\right]$ is an FPS, then we define an element $\left[x^{n}\right]\mathbf{a}\in K$ by 

\[  \left[x^{n}\right]\mathbf{a}:=a_{n}.  \]

 This is called the \emph{coefficient of }$x^{n}$\emph{ in }$\mathbf{a}$, or the $n$\emph{-th coefficient} of $\mathbf{a}$, or the $x^{n}$\emph{-coefficient} of $\mathbf{a}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.comps
def.fps.comps

\textbf{(a)} An \emph{(integer) composition} means a (finite) tuple of positive integers. \medskip 

\textbf{(b)} The \emph{size} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $\alpha _{1}+\alpha _{2}+\cdots +\alpha _{m}$. It is written $\left\vert \alpha \right\vert $. \medskip 

\textbf{(c)} The \emph{length} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $m$. It is written $\ell \left( \alpha \right) $. \medskip 

\textbf{(d)} Let $n\in \mathbb {N}$. A \emph{composition of }$n$ means a composition whose size is $n$. \medskip 

\textbf{(e)} Let $n\in \mathbb {N}$ and $k\in \mathbb {N}$. A \emph{composition of }$n$\emph{ into }$k$\emph{ parts} is a composition whose size is $n$ and whose length is $k$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.jtp.sigmaseries
def.jtp.sigmaSeries

\leanhelper  The \emph{sum-of-divisors generating function} is 

\[  S = \sum _{k>0} \sigma (k)\,  x^k \in \mathbb {Z}[[x]],  \]

 where $\sigma (k) = \sigma _1(k) = \sum _{d\mid k} d$ is the sum of positive divisors of~ $k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pars.genfun-p-s
def.pars.genFun-P-S

\leanhelper  The partition generating function $P := \sum _{n\ge 0} p(n) x^n \in \mathbb {Z}[[x]]$ and the divisor sum generating function $S := \sum _{k\ge 1} \sigma (k) x^k \in \mathbb {Z}[[x]]$.

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
  "justification": "The target quantifies exactly over natural exponents, `\u2200 (n : \u2115)`, as required by the coefficient definition, which says \u201cIf `n \u2208 \u2115`\u201d then `[x^n]a := a_n`. Its left side, `(PowerSeries.coeff n) Nat.Partition.P`, is therefore precisely `[x^n]P`. The dependency `Nat.Partition.P` has type `PowerSeries \u2124` and body `Nat.Partition.genFun fun x x_1 => 1`; by the supplied `genFun` meaning, this assigns weight 1 to every partition, so its nth coefficient counts partitions of n. The right side `\u2191(Nat.Partition.partitionCount n)` is that count cast into \u2124, matching the coefficient ring, since `partitionCount n = Fintype.card n.Partition` and `Nat.Partition` means partitions of n. Thus the formal equality expresses `[x^n]P = p(n)` for every relevant `n`."
}