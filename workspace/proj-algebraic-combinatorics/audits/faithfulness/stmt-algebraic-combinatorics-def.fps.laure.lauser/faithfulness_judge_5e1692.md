## TARGET AlgebraicCombinatorics.FPS.Laurent.laurentSeries_commRing (def) — ELABORATED SIGNATURE
{K : Type u_1} → [inst : CommRing K] → CommRing (LaurentSeries K)

Body:
fun {K} [CommRing K] => inferInstance

Docstring: **Laurent series form a commutative K-algebra**.
(Theorem thm.fps.laure.lauser-ring, label: thm.fps.laure.lauser-ring)

This is the key structural result for Laurent series. 

## TARGET AlgebraicCombinatorics.DoublyInfinitePowerSeries.IsLaurentSeries (def) — ELABORATED SIGNATURE
{K : Type u_1} → [inst : Semiring K] → AlgebraicCombinatorics.DoublyInfinitePowerSeries K → Prop

Body:
fun {K} [Semiring K] f => ∃ N, ∀ n < N, f.coeff n = 0

Docstring: A doubly infinite power series is a Laurent series if the sequence of negative
coefficients (a_{-1}, a_{-2}, a_{-3}, ...) is essentially finite, i.e., all
sufficiently negative indices have zero coefficient.

This is Definition `def.fps.laure.lauser` from the textbook:
We let K((x)) be the subset of K[[x^±]] consisting of all families (a_i)_{i∈ℤ}
such that the sequence (a_{-1}, a_{-2}, a_{-3}, ...) is essentially finite --
i.e., such that all sufficiently low i ∈ ℤ satisfy a_i = 0.

The elements of K((x)) are called Laurent series in one indeterminate x over K. 

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


## PROJECT DEPENDENCY AlgebraicCombinatorics.DoublyInfinitePowerSeries.coeff (def)
{K : Type u_1} → [inst : Semiring K] → AlgebraicCombinatorics.DoublyInfinitePowerSeries K → ℤ → K

Body:
fun {K} [Semiring K] f n => f n

Docstring: The coefficient of x^n in a doubly infinite power series 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF LaurentSeries
(R : Type u) → [Zero R] → Type (max 0 u)

Docstring: `LaurentSeries R` is the type of formal Laurent series with coefficients in `R`, denoted `R⸨X⸩`.

It is implemented as a `HahnSeries` with value group `ℤ`.


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

## BASE-LIBRARY REF inferInstance
{α : Sort u} → [i : α] → α

Docstring: `inferInstance` synthesizes a value of any target type by typeclass
inference. This function has the same type signature as the identity
function, but the square brackets on the `[i : α]` argument means that it will
attempt to construct this argument by typeclass inference. (This will fail if
`α` is not a `class`.) Example:
```
#check (inferInstance : Inhabited Nat) -- Inhabited Nat

def foo : Inhabited (Nat × Nat) :=
  inferInstance

example : foo.default = (default, default) :=
  rfl
```


## BASE-LIBRARY REF HahnSeries.instCommRing
{Γ : Type u_1} →
  {R : Type u_3} →
    [inst : AddCommMonoid Γ] →
      [inst_1 : PartialOrder Γ] → [IsOrderedCancelAddMonoid Γ] → [inst : CommRing R] → CommRing (HahnSeries Γ R)

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Int.instAddCommMonoid
AddCommMonoid ℤ

## BASE-LIBRARY REF SemilatticeInf.toPartialOrder
{α : Type u} → [self : SemilatticeInf α] → PartialOrder α

## BASE-LIBRARY REF Lattice.toSemilatticeInf
{α : Type u} → [self : Lattice α] → SemilatticeInf α

## BASE-LIBRARY REF instLatticeInt
Lattice ℤ

## BASE-LIBRARY REF Semiring
Type u → Type u

Docstring: A `Semiring` is a type with addition, multiplication, a `0` and a `1` where addition is
commutative and associative, multiplication is associative and left and right distributive over
addition, and `0` and `1` are additive and multiplicative identities. 

## BASE-LIBRARY REF Exists
{α : Sort u} → (α → Prop) → Prop

Docstring: Existential quantification. If `p : α → Prop` is a predicate, then `∃ x : α, p x`
asserts that there is some `x` of type `α` such that `p x` holds.
To create an existential proof, use the `exists` tactic,
or the anonymous constructor notation `⟨x, h⟩`.
To unpack an existential, use `cases h` where `h` is a proof of `∃ x : α, p x`,
or `let ⟨x, hx⟩ := h` where `.

Because Lean has proof irrelevance, any two proofs of an existential are
definitionally equal. One consequence of this is that it is impossible to recover the
witness of an existential from the mere fact of its existence.
For example, the following does not compile:
```
example (h : ∃ x : Nat, x = x) : Nat :=
  let ⟨x, _⟩ := h  -- fail, because the goal is `Nat : Type`
  x
```
The error message `recursor 'Exists.casesOn' can only eliminate into Prop` means
that this only works when the current goal is another proposition:
```
example (h : ∃ x : Nat, x = x) : True :=
  let ⟨x, _⟩ := h  -- ok, because the goal is `True : Prop`
  trivial
```


## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF Int.instLTInt
LT ℤ

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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF NonAssocSemiring.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonAssocSemiring α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF Semiring.toNonAssocSemiring
{α : Type u} → [self : Semiring α] → NonAssocSemiring α

## INFORMAL STATEMENT
def.fps.laure.lauser

We let $K\left( \left( x\right) \right) $ be the subset of $K\left[ \left[ x^{\pm }\right] \right] $ consisting of all families $\left( a_{i}\right) _{i\in \mathbb {Z}}\in K\left[ \left[ x^{\pm }\right] \right] $ such that the sequence $\left( a_{-1},a_{-2},a_{-3},\ldots \right) $ is essentially finite – i.e., such that all sufficiently low $i\in \mathbb {Z}$ satisfy $a_{i}=0$. 

The elements of $K\left( \left( x\right) \right) $ are called \emph{Laurent series} in one indeterminate $x$ over $K$. 

In Mathlib, Laurent series are implemented as Hahn series over $\mathbb {Z}$ with coefficients in $K$, which are functions $\mathbb {Z} \to K$ whose support is well-founded (equivalently, bounded below). The formalization also provides a predicate on doubly infinite power series that captures this textbook definition.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.infsum.essfin
def.infsum.essfin

\textbf{(a)} A family $\left(a_{i}\right)_{i\in I}\in K^{I}$ of elements of $K$ is said to be \emph{essentially finite} if all but finitely many $i\in I$ satisfy $a_{i}=0$ (in other words, if the set $\left\{ i\in I\  \mid \  a_{i}\neq 0\right\} $ is finite). \medskip 

\textbf{(b)} Let $\left(a_{i}\right)_{i\in I}\in K^{I}$ be an essentially finite family of elements of $K$. Then, the infinite sum $\sum _{i\in I}a_{i}$ is defined to equal the finite sum $\sum _{\substack {i\in I;\\ a_{i}\neq 0}}a_{i}$. Such an infinite sum is said to be \emph{essentially finite}.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The predicate target exactly formalizes the defining condition. The blueprint says \u201call sufficiently low i \u2208 \u2124 satisfy a_i = 0,\u201d while `IsLaurentSeries` has body `\u2203 N, \u2200 n < N, f.coeff n = 0`. Since `DoublyInfinitePowerSeries K` is definitionally `\u2124 \u2192 K` and `coeff f n` is `f n`, this is precisely bounded-below support, equivalently essential finiteness of `(a\u208b\u2081, a\u208b\u2082, \u2026)`. Its binder `[Semiring K]` is weaker than the commutative-ring setting inherited from the blueprint\u2019s definition of `K[[x^\u00b1]]` as a `K`-module, so this is a faithful generalization rather than an added restriction. The other target, `{K} \u2192 [CommRing K] \u2192 CommRing (LaurentSeries K)`, supplies an additional structural fact about Mathlib\u2019s `LaurentSeries K`, whose base-library definition is stated to be a Hahn-series implementation; it imposes no hypothesis beyond the blueprint\u2019s commutative-ring setting. Although its docstring calls this a commutative `K`-algebra while the signature only constructs a `CommRing`, the blueprint statement being judged does not require an algebra instance, so that wording does not create drift in the formalized definition."
}