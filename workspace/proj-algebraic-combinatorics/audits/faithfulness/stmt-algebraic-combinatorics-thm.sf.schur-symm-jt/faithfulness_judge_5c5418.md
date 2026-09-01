## TARGET SymmetricFunctions.schur_isSymmetric_jacobiTrudi (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} {R : Type u_1} [inst : CommRing R] (lam : Fin N → ℕ) (hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i),
  (SymmetricFunctions.schur { parts := lam, weaklyDecreasing := hlam }).IsSymmetric

## PROJECT DEPENDENCY SymmetricFunctions.schur (def)
{N : ℕ} → {R : Type u_1} → [inst : CommRing R] → SymmetricFunctions.NPartition N → MvPolynomial (Fin N) R

Body:
fun {N} {R} [CommRing R] lam => ∑ T ∈ SymmetricFunctions.ssytFinset lam, T.toMonomial

Docstring: The Schur polynomial s_λ defined as the sum over all SSYT of shape λ.
Definition def.sf.schur. 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.mk (constructor)
{N : ℕ} → (parts : Fin N → ℕ) → (∀ (i j : Fin N), i ≤ j → parts j ≤ parts i) → SymmetricFunctions.NPartition N

## PROJECT DEPENDENCY SymmetricFunctions.NPartition (inductive)
ℕ → Type

Body:
SymmetricFunctions.NPartition.mk : {N : ℕ} → (parts : Fin N → ℕ) → (∀ (i j : Fin N), i ≤ j → parts j ≤ parts i) → SymmetricFunctions.NPartition N

Docstring: An N-partition is a list of length N with weakly decreasing nonnegative entries.
This corresponds to Definition def.sf.N-par in the source.

**Note:** This is `SymmetricFunctions.NPartition`, a local definition.
A canonical top-level `NPartition` exists in `NPartition.lean` with the same
semantics (using `antitone` as the field name instead of `weaklyDecreasing`).
See the section docstring for details. 

## PROJECT DEPENDENCY SymmetricFunctions.SSYT (inductive)
{N : ℕ} → SymmetricFunctions.NPartition N → Type

Body:
SymmetricFunctions.SSYT.mk : {N : ℕ} →
  {lam : SymmetricFunctions.NPartition N} →
    (entries : (i : Fin N) → Fin (lam.parts i) → Fin N) →
      (∀ (i : Fin N) (j k : Fin (lam.parts i)), j ≤ k → entries i j ≤ entries i k) →
        (∀ (i : Fin N) (hi : ↑i + 1 < N) (j : Fin (lam.parts i)) (hj : ↑j < lam.parts ⟨↑i + 1, hi⟩),
            entries i j < entries ⟨↑i + 1, hi⟩ ⟨↑j, hj⟩) →
          SymmetricFunctions.SSYT lam

Docstring: A semistandard Young tableau (SSYT) of shape λ with entries in [N].
The entries are weakly increasing along rows and strictly increasing down columns.
Definition def.sf.ssyt.

**Note:** This is one of two SSYT definitions in this project:
- **This definition** (`SymmetricFunctions.SSYT`): Uses dependent types
  `entries : (i : Fin N) → (j : Fin (lam.parts i)) → Fin N`. Standalone structure.
  No `[NeZero N]` requirement. Field names: `rowWeak`, `colStrict`.
- **Alternative definition** (`SchurBasics.SSYT` in `SchurBasics.lean`): Uses
  `entry : Fin N × ℕ → Fin N` with a support condition. Extends `YoungTableau`.
  Requires `[NeZero N]`. Field names: `row_weak`, `col_strict`.

The equivalence between these definitions is established in `SSYTEquiv.lean` via
`SSYTEquiv.ssytEquiv`. Use `SSYTEquiv.toSchurBasicsSSYT` and `SSYTEquiv.toSFSSYT`
to convert between representations.

**When to use which:**
- Use this definition when the dependent type ensures bounds checking at compile time,
  or when `[NeZero N]` is not available.
- Use `SchurBasics.SSYT` when working with cell coordinates `(i, j)` directly, or when
  extending the `YoungTableau` structure is beneficial. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P_isCommRing' (def)
{K : Type u_1} → [inst : CommRing K] → {N : ℕ} → CommRing (AlgebraicCombinatorics.SymmetricPolynomials.P K N)

Body:
fun {K} [CommRing K] {N} => inferInstance

Docstring: The polynomial ring P K N is a commutative K-algebra.
Label: def.sf.PS 

## PROJECT DEPENDENCY SymmetricFunctions.ssytFinset (def)
{N : ℕ} → (lam : SymmetricFunctions.NPartition N) → Finset (SymmetricFunctions.SSYT lam)

Body:
fun {N} lam =>
  Finset.map
    {
      toFun := fun x =>
        match x with
        | ⟨f, hf⟩ => SymmetricFunctions.fillingToSSYT lam f ⋯,
      inj' := ⋯ }
    (SymmetricFunctions.ssytFillingFinsetNonSkew lam).attach

Docstring: The set of all SSYT of shape λ.
This is finite because it's a subset of all fillings, which is finite. 

## PROJECT DEPENDENCY SymmetricFunctions.SSYT.toMonomial (def)
{N : ℕ} →
  {R : Type u_1} →
    [inst : CommRing R] → {lam : SymmetricFunctions.NPartition N} → SymmetricFunctions.SSYT lam → MvPolynomial (Fin N) R

Body:
fun {N} {R} [CommRing R] {lam} T => ∏ i, ∏ j, MvPolynomial.X (T.entries i j)

Docstring: The monomial x^T associated to a tableau T.
x_T = ∏_{(i,j) ∈ Y(λ)} x_{T(i,j)} 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.parts (def)
{N : ℕ} → SymmetricFunctions.NPartition N → Fin N → ℕ

Body:
fun N self => self.1

Docstring: The parts of the partition 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P (def)
(K : Type u_2) → [CommRing K] → ℕ → Type u_2

Body:
fun K [CommRing K] N => MvPolynomial (Fin N) K

Docstring: The polynomial ring in N variables over K.
This corresponds to 𝒫 in the source (Definition def.sf.PS (a)).
Label: def.sf.PS 

## PROJECT DEPENDENCY SymmetricFunctions.Filling (def)
{N : ℕ} → SymmetricFunctions.NPartition N → Type

Body:
fun {N} lam => (i : Fin N) → Fin (lam.parts i) → Fin N

Docstring: A filling of a non-skew shape λ. 

## PROJECT DEPENDENCY SymmetricFunctions.ssytFillingFinsetNonSkew (def)
{N : ℕ} → (lam : SymmetricFunctions.NPartition N) → Finset (SymmetricFunctions.Filling lam)

Body:
fun {N} lam => Finset.filter (SymmetricFunctions.isSSYTFillingNonSkew lam) Finset.univ

Docstring: Finset of valid fillings for non-skew shapes. 

## PROJECT DEPENDENCY SymmetricFunctions.fillingToSSYT (def)
{N : ℕ} →
  (lam : SymmetricFunctions.NPartition N) →
    (f : SymmetricFunctions.Filling lam) → SymmetricFunctions.isSSYTFillingNonSkew lam f → SymmetricFunctions.SSYT lam

Body:
fun {N} lam f hf => { entries := f, rowWeak := ⋯, colStrict := ⋯ }

Docstring: Convert a valid filling to an SSYT. 

## PROJECT DEPENDENCY SymmetricFunctions.SSYT.entries (def)
{N : ℕ} →
  {lam : SymmetricFunctions.NPartition N} → SymmetricFunctions.SSYT lam → (i : Fin N) → Fin (lam.parts i) → Fin N

Body:
fun N lam self => self.1

Docstring: The entries of the tableau 

## PROJECT DEPENDENCY SymmetricFunctions.isSSYTFillingNonSkew (def)
{N : ℕ} → (lam : SymmetricFunctions.NPartition N) → SymmetricFunctions.Filling lam → Prop

Body:
fun {N} lam f => SymmetricFunctions.isRowWeakFilling lam f ∧ SymmetricFunctions.isColStrictFilling lam f

Docstring: Combined SSYT predicate for non-skew fillings. 

## PROJECT DEPENDENCY SymmetricFunctions.isSSYTFillingNonSkew_decidable (def)
{N : ℕ} →
  (lam : SymmetricFunctions.NPartition N) →
    (f : SymmetricFunctions.Filling lam) → Decidable (SymmetricFunctions.isSSYTFillingNonSkew lam f)

Body:
fun {N} lam f => instDecidableAnd

Docstring: Decidability of SSYT predicate for non-skew fillings. 

## PROJECT DEPENDENCY SymmetricFunctions.filling_fintype (def)
{N : ℕ} → (lam : SymmetricFunctions.NPartition N) → Fintype (SymmetricFunctions.Filling lam)

Body:
fun {N} lam => inferInstance

Docstring: Fintype instance for fillings of non-skew shapes. 

## PROJECT DEPENDENCY SymmetricFunctions.SSYT.mk (constructor)
{N : ℕ} →
  {lam : SymmetricFunctions.NPartition N} →
    (entries : (i : Fin N) → Fin (lam.parts i) → Fin N) →
      (∀ (i : Fin N) (j k : Fin (lam.parts i)), j ≤ k → entries i j ≤ entries i k) →
        (∀ (i : Fin N) (hi : ↑i + 1 < N) (j : Fin (lam.parts i)) (hj : ↑j < lam.parts ⟨↑i + 1, hi⟩),
            entries i j < entries ⟨↑i + 1, hi⟩ ⟨↑j, hj⟩) →
          SymmetricFunctions.SSYT lam

## PROJECT DEPENDENCY SymmetricFunctions.isRowWeakFilling (def)
{N : ℕ} → (lam : SymmetricFunctions.NPartition N) → SymmetricFunctions.Filling lam → Prop

Body:
fun {N} lam f => ∀ (i : Fin N) (j k : Fin (lam.parts i)), j ≤ k → f i j ≤ f i k

Docstring: Row-weak predicate for fillings of non-skew shapes. 

## PROJECT DEPENDENCY SymmetricFunctions.isColStrictFilling (def)
{N : ℕ} → (lam : SymmetricFunctions.NPartition N) → SymmetricFunctions.Filling lam → Prop

Body:
fun {N} lam f =>
  ∀ (i : Fin N) (hi : ↑i + 1 < N) (j : Fin (lam.parts i)) (hj : ↑j < lam.parts ⟨↑i + 1, hi⟩),
    f i j < f ⟨↑i + 1, hi⟩ ⟨↑j, hj⟩

Docstring: Column-strict predicate for fillings of non-skew shapes. 

## PROJECT DEPENDENCY SymmetricFunctions.isRowWeakFilling_decidable (def)
{N : ℕ} →
  (lam : SymmetricFunctions.NPartition N) →
    (f : SymmetricFunctions.Filling lam) → Decidable (SymmetricFunctions.isRowWeakFilling lam f)

Body:
fun {N} lam f => Fintype.decidableForallFintype

Docstring: Decidability of row-weak for non-skew fillings. 

## PROJECT DEPENDENCY SymmetricFunctions.isColStrictFilling_decidable (def)
{N : ℕ} →
  (lam : SymmetricFunctions.NPartition N) →
    (f : SymmetricFunctions.Filling lam) → Decidable (SymmetricFunctions.isColStrictFilling lam f)

Body:
fun {N} lam f => Fintype.decidableForallFintype

Docstring: Decidability of column-strict for non-skew fillings. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLEFin
{n : ℕ} → LE (Fin n)

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF MvPolynomial.IsSymmetric
{σ : Type u_1} → {R : Type u_3} → [inst : CommSemiring R] → MvPolynomial σ R → Prop

Docstring: A `MvPolynomial φ` is symmetric if it is invariant under
permutations of its variables by the `rename` operation 

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

## INFORMAL STATEMENT
thm.sf.schur-symm-jt

\leanhelper  Schur polynomials are symmetric: for any partition $\lambda $, $s_\lambda $ is a symmetric polynomial. 

This is a corollary of Theorem~ \ref{thm.sf.skew-schur-symm-jt} with $\mu = 0$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv-2eb59533
conv-2eb59533

In the Lean formalization, we use $\operatorname {Fin} n = \{ 0, 1, \ldots , n-1\} $ instead of the textbook’s $[n] = \{ 1, 2, \ldots , n\} $. Both are $n$-element sets, so their symmetric groups are isomorphic. Permutations are represented by the type of bijections $X \to X$ (denoted $\operatorname {Equiv.Perm}\,  X$ in Lean), which is a group under composition. Composition $\alpha \beta $ is the group multiplication $\alpha * \beta $, sending $x$ to $\alpha (\beta (x))$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.sn-iven
def.perm.Sn-iven

Let $n \in \mathbb {Z}$. Then, $[n]$ shall mean the set $\{ 1, 2, \ldots , n\} $. This is an $n$-element set if $n \ge 0$, and is an empty set if $n \le 0$. 

The symmetric group $S_{[n]}$ (consisting of all permutations of $[n]$) will be denoted $S_n$ and called the $n$\emph{-th symmetric group}. Its size is $n!$ (when $n \ge 0$).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.filling
def.sf.filling

\leanhelper  A \emph{filling} of a skew Young diagram $Y(\lambda /\mu )$ is a function $f : Y(\lambda /\mu ) \to [N]$. A filling is \emph{semistandard} if it satisfies the row-weak and column-strict conditions. The \emph{filling monomial} is $x_f = \prod _{c \in Y(\lambda /\mu )} x_{f(c)}$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar-order
def.sf.Npar-order

\leanhelper  We define a partial order on $N$-partitions by componentwise comparison: $\mu \leq \nu $ iff $\mu _i \leq \nu _i$ for all $i \in [N]$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar-skewyoungdiagram
def.sf.Npar-skewYoungDiagram

\leanhelper  The \emph{skew Young diagram} $Y(\lambda /\mu )$ for $N$-partitions $\lambda , \mu $ is the set difference $Y(\lambda ) \setminus Y(\mu )$, consisting of cells $(i, j)$ with $\mu _i \leq j < \lambda _i$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.schur
def.sf.schur

Let $\lambda $ be an $N$-partition. We define the \emph{Schur polynomial} $s_{\lambda }\in \mathcal{P}$ by

\[  s_{\lambda }:=\sum _{T\in \operatorname *{SSYT}\left( \lambda \right) }x_{T}.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-diag
def.sf.skew-diag

Let $\lambda $ and $\mu $ be two $N$-partitions such that $\mu \subseteq \lambda $. Then, we define the \emph{skew Young diagram} $Y\left( \lambda /\mu \right) $ to be the set difference

\begin{align*}  Y\left( \lambda \right) \setminus Y\left( \mu \right) &  =\left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \left[ \lambda _{i}\right] \setminus \left[ \mu _{i}\right] \right\}  \\ &  =\left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \mathbb {Z}\text{ and }\mu _{i}<j\leq \lambda _{i}\right\}  . \end{align*}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-ssyt
def.sf.skew-ssyt

Let $\lambda $ and $\mu $ be two $N$-partitions. 

A Young tableau $T$ of shape $\lambda /\mu $ is said to be \emph{semistandard} if its entries 

\begin{itemize} \item increase weakly along each row (from left to right); 

\item increase strictly down each column (from top to bottom). 

\end{itemize}

Formally speaking, this means that a Young tableau $T:Y\left( \lambda /\mu \right) \rightarrow \left[ N\right] $ is semistandard if and only if 

\begin{itemize} \item we have $T\left( i,j\right) \leq T\left( i,j+1\right) $ for any $\left( i,j\right) \in Y\left( \lambda /\mu \right) $ satisfying $\left( i,j+1\right) \in Y\left( \lambda /\mu \right) $; 

\item we have $T\left( i,j\right) <T\left( i+1,j\right) $ for any $\left( i,j\right) \in Y\left( \lambda /\mu \right) $ satisfying $\left( i+1,j\right) \in Y\left( \lambda /\mu \right) $. 

\end{itemize}

We let $\operatorname *{SSYT}\left( \lambda /\mu \right) $ denote the set of all semistandard Young tableaux of shape $\lambda /\mu $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-tab
def.sf.skew-tab

Let $\lambda $ and $\mu $ be two $N$-partitions such that $\mu \subseteq \lambda $. A \emph{Young tableau} of shape $\lambda /\mu $ means a way of filling the boxes of $Y\left( \lambda /\mu \right) $ with elements of $\left[ N\right] $ (one element per box). Formally speaking, it is defined as a map $T:Y\left( \lambda /\mu \right) \rightarrow \left[ N\right] $. 

Young tableaux of shape $\lambda /\mu $ are often called \emph{skew Young tableaux}. 

If we don’t have $\mu \subseteq \lambda $, then we agree that there are no Young tableaux of shape $\lambda /\mu $.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ytab.skew-xt
def.sf.ytab.skew-xT

Let $\lambda $ and $\mu $ be two $N$-partitions. If $T$ is any Young tableau of shape $\lambda /\mu $, then we define the corresponding monomial

\[  x_{T}:=\prod _{c\text{ is a box of }Y\left( \lambda /\mu \right) }x_{T\left( c\right) }=\prod _{\left( i,j\right) \in Y\left( \lambda /\mu \right) }x_{T\left( i,j\right) }=\prod _{k=1}^{N}x_{k}^{\left( \text{\#  of times }k\text{ appears in }T\right) }.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ytab.xt
def.sf.ytab.xT

Let $\lambda $ be an $N$-partition. If $T$ is any Young tableau of shape $\lambda $, then we define the corresponding monomial

\[  x_{T}:=\prod _{c\text{ is a box of }Y\left( \lambda \right) }x_{T\left( c\right) }=\prod _{\left( i,j\right) \in Y\left( \lambda \right) }x_{T\left( i,j\right) }=\prod _{k=1}^{N}x_{k}^{\left( \text{\#  of times }k\text{ appears in }T\right) }.  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint says: \u201cfor any partition \u03bb, s_\u03bb is a symmetric polynomial,\u201d in the setting of an arbitrary fixed commutative ring K and N \u2208 \u2115, with \u03bb an N-partition. The target quantifies exactly this data: `\u2200 {N : \u2115} {R : Type u_1} [inst : CommRing R] (lam : Fin N \u2192 \u2115) (hlam : \u2200 (i j : Fin N), i \u2264 j \u2192 lam j \u2264 lam i), ...`. The pair `lam` and `hlam` is precisely a weakly decreasing N-tuple of natural numbers, matching the informal N-partition definition, and it is packaged as `{ parts := lam, weaklyDecreasing := hlam }`. The referenced `schur` definition is `\u2211 T \u2208 SymmetricFunctions.ssytFinset lam, T.toMonomial`, matching `s_\u03bb := \u2211_{T \u2208 SSYT(\u03bb)} x_T`; its SSYT and monomial dependencies implement row-weak, column-strict tableaux with entries in `Fin N`, which is the declared zero-based encoding of `[N]`. Finally, the conclusion `.IsSymmetric` means invariance under permutations of variables, matching the informal definition of a symmetric polynomial. The explicit universal quantification over `N` and `R` merely makes the chapter\u2019s arbitrary fixed parameters visible and adds no restriction."
}