## TARGET AlgebraicCombinatorics.partitionGenFun_mul_pentagonalSeries (theorem) — ELABORATED SIGNATURE
AlgebraicCombinatorics.partitionGenFun * AlgebraicCombinatorics.pentagonalSeries = 1

## PROJECT DEPENDENCY AlgebraicCombinatorics.partitionGenFun (def)
PowerSeries ℤ

Body:
PowerSeries.mk fun n => ↑(AlgebraicCombinatorics.partitionCount n)

Docstring: The generating function for partitions as a formal power series.
∑_{n∈ℕ} p(n) x^n 

## PROJECT DEPENDENCY AlgebraicCombinatorics.pentagonalSeries (def)
{R : Type u_1} → [CommRing R] → PowerSeries R

Body:
fun {R} [CommRing R] => PowerSeries.mk fun n => ↑(AlgebraicCombinatorics.pentagonalCoeff n)

Docstring: The alternating sum ∑_{k∈ℤ} (-1)^k x^{w_k} as a formal power series.
This is well-defined because the pentagonal numbers grow quadratically.

We define the coefficient at n to be (-1)^k if n = w_k for some k, and 0 otherwise.
Since pentagonal numbers are injective, this is well-defined. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.partitionCount (def)
ℕ → ℕ

Body:
Nat.Partition.partitionCount

Docstring: Local alias for `Nat.Partition.partitionCount` from `Partitions/Basics.lean`.
This provides compatibility with existing code in this file. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.pentagonalCoeff (def)
ℕ → ℤ

Body:
fun n =>
  match AlgebraicCombinatorics.pentagonalNumberInverse n with
  | some k => (-1) ^ k.natAbs
  | none => 0

Docstring: The coefficient of x^n in the pentagonal series.
Returns (-1)^k if n = w_k for some k, and 0 otherwise.

Note: We use `k.natAbs` to compute the sign correctly for negative k,
since (-1)^k = (-1)^|k| for integers (as (-1)^{-m} = (-1)^m). 

## PROJECT DEPENDENCY Nat.Partition.partitionCount (def)
ℕ → ℕ

Body:
fun n => Fintype.card n.Partition

Docstring: The partition function `p(n)`: the number of partitions of `n`.
(Definition \ref{def.pars.pn-pkn} (b)) 

## PROJECT DEPENDENCY AlgebraicCombinatorics.pentagonalNumberInverse (def)
ℕ → Option ℤ

Body:
fun n =>
  have bound := n + 1;
  have posResult :=
    List.find? (fun k => decide (AlgebraicCombinatorics.pentagonalNumber k = n)) do
      let a ← List.range bound
      pure ↑a;
  match posResult with
  | some k => some k
  | none =>
    have negResult :=
      List.find? (fun k => decide (AlgebraicCombinatorics.pentagonalNumber (-k - 1) = n)) do
        let a ← List.range bound
        pure ↑a;
    match negResult with
    | some k => some (-k - 1)
    | none => none

Docstring: Helper: Check if n is a pentagonal number and return the corresponding k.
Returns none if n is not a pentagonal number.

This is computable for any given n by checking a finite range of k values,
since pentagonal numbers grow quadratically. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.pentagonalNumber (def)
ℤ → ℕ

Body:
fun k => ((3 * k - 1) * k / 2).toNat

Docstring: The k-th pentagonal number, defined as w_k = (3k - 1) * k / 2.
This is always a nonnegative integer for any k ∈ ℤ.
(Definition \ref{def.pars.pent-num}) 

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


## BASE-LIBRARY REF Int.instSemiring
Semiring ℤ

## BASE-LIBRARY REF Int.instCommRing
CommRing ℤ

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

## INFORMAL STATEMENT
lem.jtp.partitionGenFun-mul-pentagonalSeries

\leanhelper  We have $P\cdot Q = 1$, where $P=\sum _{n\geq 0}p(n)x^{n}$ is the partition generating function and $Q=\sum _{k\in \mathbb {Z}}(-1)^{k}x^{w_{k}}$ is the pentagonal series.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pars.pent-num
def.pars.pent-num

For any $k\in \mathbb {Z}$, define a nonnegative integer $w_{k}\in \mathbb {N}$ by 

\[  w_{k}=\frac{\left( 3k-1\right) k}{2}.  \]

 This is called the $k$\emph{-th pentagonal number}.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pars.pn-pkn
def.pars.pn-pkn

\textbf{(a)} Let $n\in \mathbb {Z}$ and $k\in \mathbb {N}$. Then, we set

\[  p_{k}\left( n\right) :=\left( \text{\#  of partitions of }n\text{ into }k\text{ parts}\right) .  \]

\textbf{(b)} Let $n\in \mathbb {Z}$. Then, we set

\[  p\left( n\right) :=\left( \text{\#  of partitions of }n\right) .  \]

 This is called the $n$\emph{-th partition number}.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pent.coeff
def.pent.coeff

\leanhelper  The \emph{pentagonal coefficient} at $n\in \mathbb {N}$ is 

\[  \mathrm{pentagonalCoeff}(n) = \begin{cases}  (-1)^{|k|} &  \text{if } n = w_k \text{ for some } k\in \mathbb {Z}, \\ 0 &  \text{otherwise}. \end{cases}  \]

 This is well-defined by the injectivity of pentagonal numbers (Lemma~ \ref{lem.pent.injective}).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pent.pentagonalseries
def.pent.pentagonalSeries

\leanhelper  The \emph{pentagonal series} is the formal power series 

\[  Q = \sum _{n\geq 0} \mathrm{pentagonalCoeff}(n)\,  x^n = \sum _{k\in \mathbb {Z}} (-1)^k x^{w_k} \in R[[x]].  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target states exactly `partitionGenFun * pentagonalSeries = 1`, with no added binders or hypotheses. By definition, `partitionGenFun` is `PowerSeries.mk fun n => \u2191(partitionCount n)`, and `partitionCount n` is the number of partitions of `n`, matching `P = \u2211_{n\u22650} p(n)x^n`. At the inferred coefficient ring `\u2124`, `pentagonalSeries` is `PowerSeries.mk fun n => \u2191(pentagonalCoeff n)`, where `pentagonalCoeff n` returns `(-1) ^ k.natAbs` when the inverse finds `n = w_k` and `0` otherwise. This matches the informal `Q = \u2211_{k\u2208\u2124} (-1)^k x^{w_k}`, since for base `-1`, `(-1)^{|k|} = (-1)^k`. The formal `pentagonalNumber k = ((3*k - 1)*k/2).toNat` agrees with `w_k = ((3k-1)k)/2`, which is nonnegative. Thus the formal equality is the claimed identity `P\u00b7Q = 1` in `\u2124[[x]]`."
}