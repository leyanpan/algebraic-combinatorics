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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.partitiongenfun
def.fps.partitionGenFun

\leanhelper  The \emph{partition generating function} is 

\[  P = \sum _{n\geq 0} p(n)\,  x^n \in \mathbb {Z}[[x]],  \]

 where $p(n)$ denotes the number of partitions of~ $n$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pars.odd-dist-parts
def.pars.odd-dist-parts

Let $n\in \mathbb {Z}$. \medskip 

\textbf{(a)} A \emph{partition of }$n$\emph{ into odd parts} means a partition of $n$ whose all parts are odd. \medskip 

\textbf{(b)} A \emph{partition of }$n$\emph{ into distinct parts} means a partition of $n$ whose parts are distinct. \medskip 

\textbf{(c)} Let

\begin{align*}  p_{\operatorname {odd}}\left( n\right) &  :=\left( \text{\#  of partitions of }n\text{ into odd parts}\right) \  \  \  \  \  \  \  \  \  \  \text{and}\\ p_{\operatorname {dist}}\left( n\right) &  :=\left( \text{\#  of partitions of }n\text{ into distinct parts}\right) . \end{align*}

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pars.removeone-addone
def.pars.removeOne-addOne

\leanhelper  Given a partition of $n$ that contains $1$ as a part, removing one copy of~ $1$ yields a partition of $n-1$. Conversely, adding one copy of~ $1$ to a partition of $n$ yields a partition of $n+1$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pent.coeff
def.pent.coeff

\leanhelper  The \emph{pentagonal coefficient} at $n\in \mathbb {N}$ is 

\[  \mathrm{pentagonalCoeff}(n) = \begin{cases}  (-1)^{|k|} &  \text{if } n = w_k \text{ for some } k\in \mathbb {Z}, \\ 0 &  \text{otherwise}. \end{cases}  \]

 This is well-defined by the injectivity of pentagonal numbers (Lemma~ \ref{lem.pent.injective}).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pent.pentagonalseries
def.pent.pentagonalSeries

\leanhelper  The \emph{pentagonal series} is the formal power series 

\[  Q = \sum _{n\geq 0} \mathrm{pentagonalCoeff}(n)\,  x^n = \sum _{k\in \mathbb {Z}} (-1)^k x^{w_k} \in R[[x]].  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.monomial
def.sf.monomial

\textbf{(a)} A \emph{monomial} is an expression of the form $x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ with $a_1, a_2, \ldots , a_N \in \mathbb {N}$. \medskip 

\textbf{(b)} The \emph{degree} $\deg \mathfrak {m}$ of a monomial $\mathfrak {m} = x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ is defined to be $a_1 + a_2 + \cdots + a_N \in \mathbb {N}$. \medskip 

\textbf{(c)} A monomial $\mathfrak {m} = x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ is said to be \emph{squarefree} if $a_1, a_2, \ldots , a_N \in \{ 0,1\} $. (This is saying that no square or higher power of an indeterminate appears in $\mathfrak {m}$; thus the name “squarefree”.) \medskip 

\textbf{(d)} A monomial $\mathfrak {m} = x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ is said to be \emph{primal} if there is at most one $i \in [N]$ satisfying $a_i > 0$. (This is saying that the monomial $\mathfrak {m}$ contains no two distinct indeterminates. Thus, a primal monomial is just $1$ or a power of an indeterminate.)

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar
def.sf.Npar

An $N$\emph{-partition} will mean a weakly decreasing $N$-tuple of nonnegative integers. In other words, an $N$-partition means an $N$-tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{N}\right) \in \mathbb {N}^{N}$ with $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{N}$. 

The \emph{size} (or weight) of an $N$-partition $\lambda = (\lambda _1, \lambda _2, \ldots , \lambda _N)$ is defined to be $|\lambda | := \lambda _1 + \lambda _2 + \cdots + \lambda _N$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar-youngdiagram
def.sf.Npar-youngDiagram

\leanhelper  The \emph{Young diagram} $Y(\lambda )$ of an $N$-partition $\lambda $ is the finite set of cells 

\[  Y(\lambda ) = \{ (i, j) : i \in [N],\;  0 \leq j < \lambda _i\} .  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.par-subset
def.sf.par-subset

Let $\lambda $ and $\mu $ be two $N$-partitions. 

We say that $\mu \subseteq \lambda $ if and only if $Y\left( \mu \right) \subseteq Y\left( \lambda \right) $. Equivalently, $\mu \subseteq \lambda $ if and only if

\[  \text{each }i\in \left[ N\right] \text{ satisfies }\mu _{i}\leq \lambda _{i}.  \]

 Thus we have defined a partial order $\subseteq $ on the set of all $N$-partitions.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-diag
def.sf.skew-diag

Let $\lambda $ and $\mu $ be two $N$-partitions such that $\mu \subseteq \lambda $. Then, we define the \emph{skew Young diagram} $Y\left( \lambda /\mu \right) $ to be the set difference

\begin{align*}  Y\left( \lambda \right) \setminus Y\left( \mu \right) &  =\left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \left[ \lambda _{i}\right] \setminus \left[ \mu _{i}\right] \right\}  \\ &  =\left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \mathbb {Z}\text{ and }\mu _{i}<j\leq \lambda _{i}\right\}  . \end{align*}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ssyt
def.sf.ssyt

Let $\lambda $ be an $N$-partition. 

A Young tableau $T$ of shape $\lambda $ is said to be \emph{semistandard} if its entries 

\begin{itemize} \item increase weakly along each row (from left to right); 

\item increase strictly down each column (from top to bottom). 

\end{itemize}

Formally speaking, this means that a Young tableau $T:Y\left( \lambda \right) \rightarrow \left[ N\right] $ is semistandard if and only if 

\begin{itemize} \item we have $T\left( i,j\right) \leq T\left( i,j+1\right) $ for any $\left( i,j\right) \in Y\left( \lambda \right) $ satisfying $\left( i,j+1\right) \in Y\left( \lambda \right) $; 

\item we have $T\left( i,j\right) <T\left( i+1,j\right) $ for any $\left( i,j\right) \in Y\left( \lambda \right) $ satisfying $\left( i+1,j\right) \in Y\left( \lambda \right) $. 

\end{itemize}

We let $\operatorname *{SSYT}\left( \lambda \right) $ denote the set of all semistandard Young tableaux of shape $\lambda $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.strips
def.sf.strips

Let $\lambda $ and $\mu $ be two $N$-partitions. 

\textbf{(a)} We write $\lambda /\mu $ for the pair $\left( \mu ,\lambda \right) $. Such a pair is called a \emph{skew partition}. 

\textbf{(b)} We say that $\lambda /\mu $ is a \emph{horizontal strip} if we have $\mu \subseteq \lambda $ and the Young diagram $Y\left( \lambda /\mu \right) $ has no two boxes lying in the same column. 

\textbf{(c)} We say that $\lambda /\mu $ is a \emph{vertical strip} if we have $\mu \subseteq \lambda $ and the Young diagram $Y\left( \lambda /\mu \right) $ has no two boxes lying in the same row. 

Now, let $n\in \mathbb {N}$. 

\textbf{(d)} We say that $\lambda /\mu $ is a \emph{horizontal }$n$\emph{-strip} if $\lambda /\mu $ is a horizontal strip and satisfies $\left\vert Y\left( \lambda /\mu \right) \right\vert =n$. 

\textbf{(e)} We say that $\lambda /\mu $ is a \emph{vertical }$n$\emph{-strip} if $\lambda /\mu $ is a vertical strip and satisfies $\left\vert Y\left( \lambda /\mu \right) \right\vert =n$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ydiag
def.sf.ydiag

Let $\lambda $ be an $N$-partition. 

The \emph{Young diagram} of $\lambda $ is defined as the set

\[  \left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \left[ \lambda _{i}\right] \right\}  \subseteq \left\{  1,2,3,\ldots \right\}  ^{2}.  \]

 We visually represent each element $\left( i,j\right) $ of this Young diagram as a box in row $i$ and column $j$. 

We denote the Young diagram of $\lambda $ by $Y\left( \lambda \right) $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ytab
def.sf.ytab

Let $\lambda $ be an $N$-partition. 

A \emph{Young tableau} of shape $\lambda $ means a way of filling the boxes of $Y\left( \lambda \right) $ with elements of $\left[ N\right] $ (one element per box). Formally speaking, it is defined as a map $T:Y\left( \lambda \right) \rightarrow \left[ N\right] $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ytab.xt
def.sf.ytab.xT

Let $\lambda $ be an $N$-partition. If $T$ is any Young tableau of shape $\lambda $, then we define the corresponding monomial

\[  x_{T}:=\prod _{c\text{ is a box of }Y\left( \lambda \right) }x_{T\left( c\right) }=\prod _{\left( i,j\right) \in Y\left( \lambda \right) }x_{T\left( i,j\right) }=\prod _{k=1}^{N}x_{k}^{\left( \text{\#  of times }k\text{ appears in }T\right) }.  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target states exactly `AlgebraicCombinatorics.partitionGenFun * AlgebraicCombinatorics.pentagonalSeries = 1`, with no added binders or hypotheses. Here `partitionGenFun` is the integer power series `PowerSeries.mk fun n => \u2191(partitionCount n)`, and `partitionCount n` is `Fintype.card n.Partition`, matching `P = \u2211_{n\u22650} p(n)x^n \u2208 \u2124[[x]]`. The polymorphic `pentagonalSeries` is inferred at `R = \u2124` in this product and has coefficient `pentagonalCoeff n`, which is `(-1) ^ k.natAbs` when `pentagonalNumberInverse n = some k` and zero otherwise. This matches the blueprint definition `pentagonalCoeff(n) = (-1)^{|k|}` when `n = w_k`, with `pentagonalNumber k = ((3*k - 1)*k/2).toNat` matching `w_k = ((3k-1)k)/2`. Thus the formal equality is precisely the asserted identity `P\u00b7Q = 1` in `\u2124[[x]]`."
}