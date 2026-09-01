## TARGET rhoVector_sum (theorem) — ELABORATED SIGNATURE
∀ (N : ℕ), ∑ i, rhoVector N i = N * (N - 1) / 2

Docstring: The sum of the ρ vector equals N(N-1)/2, which is the triangular number T_{N-1}.
This follows from ∑_{i=0}^{N-1} (N-1-i) = ∑_{k=0}^{N-1} k = N(N-1)/2. 

## PROJECT DEPENDENCY rhoVector (def)
(N : ℕ) → Fin N → ℕ

Body:
fun N => AlgebraicCombinatorics.rho N

Docstring: The ρ vector is the N-tuple (N-1, N-2, ..., 0).
Definition \ref{def.sf.alternants}(a) in the source.

Note: The textbook uses 1-based indexing with ρ_j = N - j for j ∈ [N].
In Lean with 0-based indexing, this becomes ρ(i) = N - 1 - i for i ∈ Fin N.

This is an abbreviation for `AlgebraicCombinatorics.rho N` from LittlewoodRichardson.lean. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.rho (def)
(N : ℕ) → Fin N → ℕ

Body:
fun N i => N - 1 - ↑i

Docstring: The staircase partition ρ = (N-1, N-2, ..., 1, 0). 

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

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF HDiv.hDiv
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HDiv α β γ] → α → β → γ

Docstring: `a / b` computes the result of dividing `a` by `b`.
The meaning of this notation is type-dependent.
* For most types like `Nat`, `Int`, `Rat`, `Real`, `a / 0` is defined to be `0`.
* For `Nat`, `a / b` rounds downwards.
* For `Int`, `a / b` rounds downwards if `b` is positive or upwards if `b` is negative.
  It is implemented as `Int.ediv`, the unique function satisfying
  `a % b + b * (a / b) = a` and `0 ≤ a % b < natAbs b` for `b ≠ 0`.
  Other rounding conventions are available using the functions
  `Int.fdiv` (floor rounding) and `Int.tdiv` (truncation rounding).
* For `Float`, `a / 0` follows the IEEE 754 semantics for division,
  usually resulting in `inf` or `nan`. 

Conventions for notations in identifiers:

 * The recommended spelling of `/` in identifiers is `div`.

## BASE-LIBRARY REF instHDiv
{α : Type u_1} → [Div α] → HDiv α α α

## BASE-LIBRARY REF Nat.instDiv
Div ℕ

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

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF instSubNat
Sub ℕ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## INFORMAL STATEMENT
lem.sf.rhoVector-sum

\leanhelper  The sum of the $\rho $ vector equals the triangular number: 

\[  \sum _{i=0}^{N-1} \rho _i = \frac{N(N-1)}{2}.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.det.matrices
conv.det.matrices

Let $n, m \in \mathbb {N}$. 

\textbf{(a)} If $A$ is an $n \times m$-matrix, then $A_{i,j}$ shall mean the $(i,j)$-th entry of $A$, that is, the entry of $A$ in row $i$ and column $j$. 

\textbf{(b)} If $a_{i,j}$ is an element of $K$ for each $i \in [n]$ and each $j \in [m]$, then 

\[  \left( a_{i,j} \right)_{1 \leq i \leq n,\;  1 \leq j \leq m}  \]

 shall denote the $n \times m$-matrix whose $(i,j)$-th entry is $a_{i,j}$ for all $i \in [n]$ and $j \in [m]$. 

\textbf{(c)} We let $K^{n \times m}$ denote the set of all $n \times m$-matrices with entries in $K$. This is a $K$-module. If $n = m$, this is also a $K$-algebra. 

\textbf{(d)} Let $A \in K^{n \times m}$ be an $n \times m$-matrix. The \emph{transpose} $A^T$ of $A$ is defined to be the $m \times n$-matrix whose entries are given by 

\[  \left( A^T \right)_{i,j} = A_{j,i} \quad \text{for all } i \in [m] \text{ and } j \in [n].  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.sf.kn
conv.sf.KN

Fix a commutative ring $K$. Fix an $N\in \mathbb {N}$. Throughout this chapter, we will keep $K$ and $N$ fixed. Let $S_N$ denote the symmetric group, i.e., the group of all permutations of $[N] := \{ 1,2,\ldots ,N\} $.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.alg.kalg
def.alg.Kalg

A $K$\emph{-algebra} is a set $A$ equipped with four maps

\begin{align*}  \oplus &  :A\times A\rightarrow A,\\ \ominus &  :A\times A\rightarrow A,\\ \odot &  :A\times A\rightarrow A,\\ \rightharpoonup &  :K\times A\rightarrow A \end{align*}

 and two elements $\overrightarrow {0}\in A$ and $\overrightarrow {1}\in A$ satisfying the following properties: 

\begin{enumerate} \item The set $A$, equipped with the maps $\oplus $, $\ominus $ and $\odot $ and the two elements $\overrightarrow {0}$ and $\overrightarrow {1}$, is a (noncommutative) ring. 

\item The set $A$, equipped with the maps $\oplus $, $\ominus $ and $\rightharpoonup $ and the element $\overrightarrow {0}$, is a $K$-module. 

\item We have

\begin{equation}  \lambda \rightharpoonup \left( a\odot b\right) =\left( \lambda \rightharpoonup a\right) \odot b=a\odot \left( \lambda \rightharpoonup b\right) \end{equation}

 for all $\lambda \in K$ and $a,b\in A$. 

\end{enumerate}

(Thus, in a nutshell, a $K$-algebra is a set $A$ that is simultaneously a ring and a $K$-module, with the property that the ring $A$ and the $K$-module $A$ have the same addition, the same subtraction and the same zero, and satisfy the additional compatibility property (\ref{eq.def.alg.Kalg.scaleinv}).)

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.alg.ring
def.alg.ring

The notion of a \emph{ring} (also known as a \emph{noncommutative ring}) is defined in the exact same way as we defined the notion of a commutative ring in Definition~ \ref{def.alg.commring}, except that the “Commutativity of multiplication” axiom is removed.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.det.det
def.det.det

Let $n \in \mathbb {N}$. Let $A \in K^{n \times n}$ be an $n \times n$-matrix. The \emph{determinant} $\det A$ of $A$ is defined to be the element 

\[  \sum _{\sigma \in S_n} (-1)^{\sigma } \underbrace{A_{1,\sigma (1)} A_{2,\sigma (2)} \cdots A_{n,\sigma (n)}}_{ = \prod _{i=1}^{n} A_{i,\sigma (i)}}  \]

 of $K$. Here: 

\begin{itemize} \item we let $S_n$ denote the $n$-th symmetric group (i.e., the group of permutations of $[n] = \{ 1, 2, \ldots , n\} $); 

\item we let $(-1)^{\sigma }$ denote the sign of the permutation $\sigma $ (as defined in Definition~ \ref{def.perm.sign}). 

\end{itemize}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.invs
def.perm.invs

Let $n\in \mathbb {N}$ and $\sigma \in S_{n}$. \medskip 

\textbf{(a)} An \emph{inversion} of $\sigma $ means a pair $\left(i,j\right)$ of elements of $\left[n\right]$ such that $i<j$ and $\sigma \left(i\right) >\sigma \left(j\right)$. \medskip 

\textbf{(b)} The \emph{length} (also known as the \emph{Coxeter length}) of $\sigma $ is the \#  of inversions of $\sigma $. It is called $\ell \left( \sigma \right)$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.sign
def.perm.sign

Let $n \in \mathbb {N}$. The \emph{sign} of a permutation $\sigma \in S_n$ is defined to be the integer $(-1)^{\ell (\sigma )}$. 

It is denoted by $(-1)^{\sigma }$ or $\operatorname {sgn}(\sigma )$ or $\operatorname {sign}(\sigma )$ or $\varepsilon (\sigma )$. It is also known as the \emph{signature} of $\sigma $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.sn-iven
def.perm.Sn-iven

Let $n \in \mathbb {Z}$. Then, $[n]$ shall mean the set $\{ 1, 2, \ldots , n\} $. This is an $n$-element set if $n \ge 0$, and is an empty set if $n \le 0$. 

The symmetric group $S_{[n]}$ (consisting of all permutations of $[n]$) will be denoted $S_n$ and called the $n$\emph{-th symmetric group}. Its size is $n!$ (when $n \ge 0$).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.alternants
def.sf.alternants

\textbf{(a)} We let $\rho $ be the $N$-tuple $\left( N-1,N-2,\ldots ,N-N\right) \in \mathbb {N}^{N}$. \medskip 

\textbf{(b)} For any $N$-tuple $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{N}\right) \in \mathbb {N}^{N}$, we define

\[  a_{\alpha }:=\det \left( \underbrace{\left( x_{i}^{\alpha _{j}}\right) _{1\leq i\leq N,\  1\leq j\leq N}}_{\in \mathcal{P}^{N\times N}}\right) \in \mathcal{P}.  \]

 This is called the $\alpha $\emph{-alternant} (of $x_{1},x_{2},\ldots ,x_{N}$).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ps
def.sf.PS

\textbf{(a)} Let $\mathcal{P}$ be the polynomial ring $K[x_1, x_2, \ldots , x_N]$ in $N$ variables over $K$. This is not just a ring; it is a commutative $K$-algebra. \medskip 

\textbf{(b)} The symmetric group $S_N$ acts on the set $\mathcal{P}$ according to the formula 

\[  \sigma \cdot f = f[x_{\sigma (1)}, x_{\sigma (2)}, \ldots , x_{\sigma (N)}] \quad \text{for any } \sigma \in S_N \text{ and any } f \in \mathcal{P}.  \]

 Here, $f[a_1, a_2, \ldots , a_N]$ means the result of substituting $a_1, a_2, \ldots , a_N$ for the indeterminates $x_1, x_2, \ldots , x_N$ in a polynomial $f \in \mathcal{P}$. 

Roughly speaking, the group $S_N$ is thus acting on $\mathcal{P}$ by permuting variables: A permutation $\sigma \in S_N$ transforms a polynomial $f$ by substituting $x_{\sigma (i)}$ for each $x_i$. 

Note that this action of $S_N$ on $\mathcal{P}$ is a well-defined group action (as we will see in Proposition~ \ref{prop.sf.SN-acts} below). \medskip 

\textbf{(c)} A polynomial $f \in \mathcal{P}$ is said to be \emph{symmetric} if it satisfies 

\[  \sigma \cdot f = f \quad \text{for all } \sigma \in S_N.  \]

\textbf{(d)} We let $\mathcal{S}$ be the set of all symmetric polynomials $f \in \mathcal{P}$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal theorem quantifies over exactly the required parameter, `\u2200 (N : \u2115)`, with no added hypotheses. Its summand expands through `rhoVector N i = AlgebraicCombinatorics.rho N i` to `N - 1 - \u2191i` for `i : Fin N`, so `\u2211 i, rhoVector N i` sums the entries `(N-1, N-2, \u2026, 0)` over all `N` indices. This is precisely the informal definition \u201cWe let \u03c1 be the N-tuple `(N-1,N-2,\u2026,N-N)`\u201d and the claimed sum `\u2211_{i=0}^{N-1} \u03c1_i`. The conclusion `= N * (N - 1) / 2` is the same triangular-number formula `N(N-1)/2`; all operations are on `\u2115`, and the numerator is even, so natural-number division does not alter the intended value."
}