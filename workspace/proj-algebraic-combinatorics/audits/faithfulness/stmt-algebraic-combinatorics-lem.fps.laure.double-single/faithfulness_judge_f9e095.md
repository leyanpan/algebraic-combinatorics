## TARGET AlgebraicCombinatorics.DoublyInfinitePowerSeries.coeff_single (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : Semiring K] (n m : ℤ),
  (AlgebraicCombinatorics.DoublyInfinitePowerSeries.single n).coeff m = if m = n then 1 else 0

## TARGET AlgebraicCombinatorics.DoublyInfinitePowerSeries.single (def) — ELABORATED SIGNATURE
{K : Type u_1} → [inst : Semiring K] → ℤ → AlgebraicCombinatorics.DoublyInfinitePowerSeries K

Body:
fun {K} [Semiring K] n m => if m = n then 1 else 0

Docstring: The element x^n in K[[x^±]], represented as a family 

## TARGET AlgebraicCombinatorics.DoublyInfinitePowerSeries.smul_single (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : Semiring K] (r : K) (n : ℤ),
  r • AlgebraicCombinatorics.DoublyInfinitePowerSeries.single n = fun m => if m = n then r else 0

Docstring: Scalar multiplication of single. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.DoublyInfinitePowerSeries.coeff (def)
{K : Type u_1} → [inst : Semiring K] → AlgebraicCombinatorics.DoublyInfinitePowerSeries K → ℤ → K

Body:
fun {K} [Semiring K] f n => f n

Docstring: The coefficient of x^n in a doubly infinite power series 

## PROJECT DEPENDENCY AlgebraicCombinatorics.DoublyInfinitePowerSeries (def)
(K : Type u_1) → [Semiring K] → Type u_1

Body:
fun K [Semiring K] => ℤ → K

Docstring: The K-module of doubly infinite power series K[[x^±]].

An element is a family `(a_n)_{n ∈ ℤ}` of elements of K. Addition and scalar
multiplication are defined entrywise.

Note: This is NOT a ring because multiplication is not always well-defined
(the convolution sum may be infinite).

This corresponds to Definition `def.fps.laure.double`.


## PROJECT DEPENDENCY AlgebraicCombinatorics.DoublyInfinitePowerSeries.instAddCommMonoid (def)
{K : Type u_1} → [inst : Semiring K] → AddCommMonoid (AlgebraicCombinatorics.DoublyInfinitePowerSeries K)

Body:
fun {K} [Semiring K] => Pi.addCommMonoid

## PROJECT DEPENDENCY AlgebraicCombinatorics.DoublyInfinitePowerSeries.instModule (def)
{K : Type u_1} → [inst : Semiring K] → _root_.Module K (AlgebraicCombinatorics.DoublyInfinitePowerSeries K)

Body:
fun {K} [Semiring K] => Pi.module ℤ (fun a => K) K

## BASE-LIBRARY REF Semiring
Type u → Type u

Docstring: A `Semiring` is a type with addition, multiplication, a `0` and a `1` where addition is
commutative and associative, multiplication is associative and left and right distributive over
addition, and `0` and `1` are additive and multiplicative identities. 

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

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF Int.instDecidableEq
DecidableEq ℤ

Docstring: Decides whether two integers are equal. Usually accessed via the `DecidableEq Int` instance.

This function is overridden by the compiler with an efficient implementation. This definition is the
logical model.

Examples:
* `show (7 : Int) = (3 : Int) + (4 : Int) by decide`
* `if (6 : Int) = (3 : Int) * (2 : Int) then "yes" else "no" = "yes"`
* `(¬ (6 : Int) = (3 : Int)) = true`


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

## BASE-LIBRARY REF AddCommMonoidWithOne.toAddMonoidWithOne
{R : Type u_2} → [self : AddCommMonoidWithOne R] → AddMonoidWithOne R

## BASE-LIBRARY REF NonAssocSemiring.toAddCommMonoidWithOne
{α : Type u} → [self : NonAssocSemiring α] → AddCommMonoidWithOne α

## BASE-LIBRARY REF Semiring.toNonAssocSemiring
{α : Type u} → [self : Semiring α] → NonAssocSemiring α

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toMulZeroClass
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → MulZeroClass α

## BASE-LIBRARY REF NonAssocSemiring.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonAssocSemiring α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF HSMul.hSMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSMul α β γ] → α → β → γ

Docstring: `a • b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent, but it is intended to be used for left actions. 

Conventions for notations in identifiers:

 * The recommended spelling of `•` in identifiers is `smul`.

## BASE-LIBRARY REF instHSMul
{α : Type u_1} → {β : Type u_2} → [SMul α β] → HSMul α β β

## BASE-LIBRARY REF SMulZeroClass.toSMul
{M : Type u_12} → {A : Type u_13} → {inst : Zero A} → [self : SMulZeroClass M A] → SMul M A

## BASE-LIBRARY REF AddZero.toZero
{M : Type u_2} → [self : AddZero M] → Zero M

## BASE-LIBRARY REF AddZeroClass.toAddZero
{M : Type u} → [self : AddZeroClass M] → AddZero M

## BASE-LIBRARY REF AddMonoid.toAddZeroClass
{M : Type u} → [self : AddMonoid M] → AddZeroClass M

## BASE-LIBRARY REF AddCommMonoid.toAddMonoid
{M : Type u} → [self : AddCommMonoid M] → AddMonoid M

## BASE-LIBRARY REF DistribSMul.toSMulZeroClass
{M : Type u_12} → {A : Type u_13} → {inst : AddZeroClass A} → [self : DistribSMul M A] → SMulZeroClass M A

## BASE-LIBRARY REF DistribMulAction.toDistribSMul
{M : Type u_1} → {A : Type u_7} → [inst : Monoid M] → [inst_1 : AddMonoid A] → [DistribMulAction M A] → DistribSMul M A

## BASE-LIBRARY REF MonoidWithZero.toMonoid
{M₀ : Type u} → [self : MonoidWithZero M₀] → Monoid M₀

## BASE-LIBRARY REF Semiring.toMonoidWithZero
{α : Type u} → [self : Semiring α] → MonoidWithZero α

## BASE-LIBRARY REF Module.toDistribMulAction
{R : Type u} →
  {M : Type v} → {inst : Semiring R} → {inst_1 : AddCommMonoid M} → [self : _root_.Module R M] → DistribMulAction R M

## BASE-LIBRARY REF AddCommMonoid
Type u → Type u

Docstring: An additive commutative monoid is an additive monoid with commutative `(+)`. 

## BASE-LIBRARY REF Pi.addCommMonoid
{I : Type u} → {f : I → Type v₁} → [(i : I) → AddCommMonoid (f i)] → AddCommMonoid ((i : I) → f i)

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toAddCommMonoid
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → AddCommMonoid α

## BASE-LIBRARY REF Module
(R : Type u) → (M : Type v) → [Semiring R] → [AddCommMonoid M] → Type (max u v)

Docstring: A module is a generalization of vector spaces to a scalar semiring.
It consists of a scalar semiring `R` and an additive monoid of "vectors" `M`,
connected by a "scalar multiplication" operation `r • x : M`
(where `r : R` and `x : M`) with some natural associativity and
distributivity axioms similar to those on a ring. 

## BASE-LIBRARY REF Pi.module
(I : Type u) →
  (f : I → Type v) →
    (α : Type u_1) →
      {r : Semiring α} →
        {m : (i : I) → AddCommMonoid (f i)} → [(i : I) → _root_.Module α (f i)] → _root_.Module α ((i : I) → f i)

## BASE-LIBRARY REF Semiring.toModule
{R : Type u_1} → [inst : Semiring R] → _root_.Module R R

## INFORMAL STATEMENT
Single monomials in K[[x±]]

\! ]$]   \leanhelper  For $n \in \mathbb {Z}$, the monomial $x^n \in K[\! [x^{\pm }]\! ]$ is the family $(\delta _{m,n})_{m \in \mathbb {Z}}$. Its coefficient at $m$ is $\delta _{m,n}$. Scalar multiplication satisfies $\lambda \cdot x^n = (\lambda \delta _{m,n})_{m \in \mathbb {Z}}$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.laure.double
def.fps.laure.double

Let $K\left[ \left[ x^{\pm }\right] \right] $ be the $K$-module $K^{\mathbb {Z}}$ of all families $\left( a_{n}\right) _{n\in \mathbb {Z}}=\left( \ldots ,a_{-2},a_{-1},a_{0},a_{1},a_{2},\ldots \right) $ of elements of $K$. Its addition and its scaling are defined entrywise:

\begin{align*}  \left( a_{n}\right) _{n\in \mathbb {Z}}+\left( b_{n}\right) _{n\in \mathbb {Z}} &  =\left( a_{n}+b_{n}\right) _{n\in \mathbb {Z}};\\ \lambda \left( a_{n}\right) _{n\in \mathbb {Z}} &  =\left( \lambda a_{n}\right) _{n\in \mathbb {Z}}\  \  \  \  \  \  \  \  \  \  \text{for each }\lambda \in K. \end{align*}

 An element of $K\left[ \left[ x^{\pm }\right] \right] $ will be called a \emph{doubly infinite power series}. We use the notation $\sum _{n\in \mathbb {Z}}a_{n}x^{n}$ for a family $\left( a_{n}\right) _{n\in \mathbb {Z}}\in K\left[ \left[ x^{\pm }\right] \right] $.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal declarations exactly realize the three blueprint claims. `single` has body `fun ... n m => if m = n then 1 else 0`, which is the family `(\u03b4_{m,n})_{m \u2208 \u2124}`. `coeff_single` states `(single n).coeff m = if m = n then 1 else 0`, matching \u201cIts coefficient at m is \u03b4_{m,n},\u201d since `coeff` is defined by evaluation: `fun ... f n => f n`. Finally, `smul_single` states `r \u2022 single n = fun m => if m = n then r else 0`, matching `\u03bb \u00b7 x^n = (\u03bb \u03b4_{m,n})_{m \u2208 \u2124}` under the entrywise `Pi.module` action. The formal binder `[Semiring K]` is weaker than the blueprint\u2019s commutative-ring setting, allowing semirings and noncommutative multiplication; this is a harmless strict generalization, not an added restriction, and therefore remains faithful."
}