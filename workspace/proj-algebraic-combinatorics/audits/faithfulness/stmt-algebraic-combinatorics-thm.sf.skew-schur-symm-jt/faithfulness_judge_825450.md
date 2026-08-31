## TARGET SymmetricFunctions.skewSchur_isSymmetric_jacobiTrudi (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} {R : Type u_1} [inst : CommRing R] (lam mu : Fin N → ℕ) (hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i)
  (hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i) (hcontained : ∀ (i : Fin N), mu i ≤ lam i),
  (SymmetricFunctions.skewSchur
      { outer := { parts := lam, weaklyDecreasing := hlam }, inner := { parts := mu, weaklyDecreasing := hmu },
        contained := ⋯ }).IsSymmetric

## PROJECT DEPENDENCY SymmetricFunctions.skewSchur (def)
{N : ℕ} → {R : Type u_1} → [inst : CommRing R] → SymmetricFunctions.SkewPartition N → MvPolynomial (Fin N) R

Body:
fun {N} {R} [CommRing R] s => ∑ T ∈ SymmetricFunctions.skewSSYTFinset s, T.toMonomial

Docstring: The skew Schur polynomial s_{λ/μ} defined as the sum over all skew SSYT.
Definition def.sf.skew-schur. 

## PROJECT DEPENDENCY SymmetricFunctions.SkewPartition.mk (constructor)
{N : ℕ} → (outer inner : SymmetricFunctions.NPartition N) → inner ≤ outer → SymmetricFunctions.SkewPartition N

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.mk (constructor)
{N : ℕ} → (parts : Fin N → ℕ) → (∀ (i j : Fin N), i ≤ j → parts j ≤ parts i) → SymmetricFunctions.NPartition N

## PROJECT DEPENDENCY SymmetricFunctions.SkewPartition (inductive)
ℕ → Type

Body:
SymmetricFunctions.SkewPartition.mk : {N : ℕ} → (outer inner : SymmetricFunctions.NPartition N) → inner ≤ outer → SymmetricFunctions.SkewPartition N

Docstring: A skew partition λ/μ is a pair of N-partitions with μ ⊆ λ.
Definition def.sf.strips(a). 

## PROJECT DEPENDENCY SymmetricFunctions.SkewSSYT (inductive)
{N : ℕ} → SymmetricFunctions.SkewPartition N → Type

Body:
SymmetricFunctions.SkewSSYT.mk : {N : ℕ} →
  {s : SymmetricFunctions.SkewPartition N} →
    (entries : (i : Fin N) → Fin (s.outer.parts i - s.inner.parts i) → Fin N) →
      (∀ (i : Fin N) (j k : Fin (s.outer.parts i - s.inner.parts i)), j ≤ k → entries i j ≤ entries i k) →
        (∀ (i : Fin N) (hi : ↑i + 1 < N) (k : Fin (s.outer.parts i - s.inner.parts i)),
            s.inner.parts i + ↑k + 1 > s.inner.parts ⟨↑i + 1, hi⟩ ∧
                s.inner.parts i + ↑k + 1 ≤ s.outer.parts ⟨↑i + 1, hi⟩ →
              let k' := s.inner.parts i + ↑k - s.inner.parts ⟨↑i + 1, hi⟩;
              ∀ (hk' : k' < s.outer.parts ⟨↑i + 1, hi⟩ - s.inner.parts ⟨↑i + 1, hi⟩),
                entries i k < entries ⟨↑i + 1, hi⟩ ⟨k', hk'⟩) →
          SymmetricFunctions.SkewSSYT s

Docstring: A semistandard Young tableau of skew shape λ/μ with entries in [N].
Definition def.sf.skew-schur.

For a skew tableau, the column-strict condition requires that entries
are strictly increasing down columns, where column j of Y(λ/μ) consists
of boxes (i, j) with μᵢ < j ≤ λᵢ.

**Note:** This is one of two SkewSSYT definitions in this project:
- **This definition** (`SymmetricFunctions.SkewSSYT`): Uses dependent types. Takes
  `s : SkewPartition N` as a single bundled argument. No `[NeZero N]` requirement.
  Field names: `rowWeak`, `colStrict`.
- **Alternative definition** (`SchurBasics.SkewSSYT` in `SchurBasics.lean`): Uses
  `entry : Fin N × ℕ → Fin N` with a support condition. Extends `SkewYoungTableau`.
  Takes `lam mu : NPartition N` as separate arguments. Requires `[NeZero N]`.
  Field names: `row_weak`, `col_strict`.

See `SSYTEquiv.lean` for conversions between representations. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P_isCommRing' (def)
{K : Type u_1} → [inst : CommRing K] → {N : ℕ} → CommRing (AlgebraicCombinatorics.SymmetricPolynomials.P K N)

Body:
fun {K} [CommRing K] {N} => inferInstance

Docstring: The polynomial ring P K N is a commutative K-algebra.
Label: def.sf.PS 

## PROJECT DEPENDENCY SymmetricFunctions.skewSSYTFinset (def)
{N : ℕ} → (s : SymmetricFunctions.SkewPartition N) → Finset (SymmetricFunctions.SkewSSYT s)

Body:
fun {N} s =>
  Finset.map
    {
      toFun := fun x =>
        match x with
        | ⟨f, hf⟩ => SymmetricFunctions.fillingToSkewSSYT f ⋯,
      inj' := ⋯ }
    (SymmetricFunctions.ssytFillingFinset s).attach

Docstring: The set of all skew SSYT of shape λ/μ.
This is finite because it's a subset of all fillings, which is finite. 

## PROJECT DEPENDENCY SymmetricFunctions.SkewSSYT.toMonomial (def)
{N : ℕ} →
  {R : Type u_1} →
    [inst : CommRing R] →
      {s : SymmetricFunctions.SkewPartition N} → SymmetricFunctions.SkewSSYT s → MvPolynomial (Fin N) R

Body:
fun {N} {R} [CommRing R] {s} T => ∏ i, ∏ j, MvPolynomial.X (T.entries i j)

Docstring: The monomial x^T associated to a skew tableau T. 

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

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.instLE (def)
{N : ℕ} → LE (SymmetricFunctions.NPartition N)

Body:
fun {N} => { le := SymmetricFunctions.NPartition.partLE }

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.parts (def)
{N : ℕ} → SymmetricFunctions.NPartition N → Fin N → ℕ

Body:
fun N self => self.1

Docstring: The parts of the partition 

## PROJECT DEPENDENCY SymmetricFunctions.SkewPartition.outer (def)
{N : ℕ} → SymmetricFunctions.SkewPartition N → SymmetricFunctions.NPartition N

Body:
fun N self => self.1

Docstring: The outer partition λ 

## PROJECT DEPENDENCY SymmetricFunctions.SkewPartition.inner (def)
{N : ℕ} → SymmetricFunctions.SkewPartition N → SymmetricFunctions.NPartition N

Body:
fun N self => self.2

Docstring: The inner partition μ 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P (def)
(K : Type u_2) → [CommRing K] → ℕ → Type u_2

Body:
fun K [CommRing K] N => MvPolynomial (Fin N) K

Docstring: The polynomial ring in N variables over K.
This corresponds to 𝒫 in the source (Definition def.sf.PS (a)).
Label: def.sf.PS 

## PROJECT DEPENDENCY SymmetricFunctions.SkewFilling (def)
{N : ℕ} → SymmetricFunctions.SkewPartition N → Type

Body:
fun {N} s => (i : Fin N) → Fin (s.outer.parts i - s.inner.parts i) → Fin N

Docstring: A filling of a skew shape is a function assigning a value in Fin N to each cell.
We use `abbrev` instead of `def` to ensure type class inference can see through this. 

## PROJECT DEPENDENCY SymmetricFunctions.ssytFillingFinset (def)
{N : ℕ} → (s : SymmetricFunctions.SkewPartition N) → Finset (SymmetricFunctions.SkewFilling s)

Body:
fun {N} s => Finset.filter (SymmetricFunctions.isSSYTFilling s) Finset.univ

Docstring: The finite set of all fillings satisfying SSYT conditions. 

## PROJECT DEPENDENCY SymmetricFunctions.fillingToSkewSSYT (def)
{N : ℕ} →
  {s : SymmetricFunctions.SkewPartition N} →
    (f : SymmetricFunctions.SkewFilling s) → SymmetricFunctions.isSSYTFilling s f → SymmetricFunctions.SkewSSYT s

Body:
fun {N} {s} f hf => { entries := f, rowWeak := ⋯, colStrict := ⋯ }

Docstring: A filling satisfying SSYT conditions can be converted to a SkewSSYT. 

## PROJECT DEPENDENCY SymmetricFunctions.SkewSSYT.entries (def)
{N : ℕ} →
  {s : SymmetricFunctions.SkewPartition N} →
    SymmetricFunctions.SkewSSYT s → (i : Fin N) → Fin (s.outer.parts i - s.inner.parts i) → Fin N

Body:
fun N s self => self.1

Docstring: The entries of the tableau, only for boxes in Y(λ/μ).
Entry (i, k) corresponds to box (i, μᵢ + k + 1) in Y(λ/μ). 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.partLE (def)
{N : ℕ} → SymmetricFunctions.NPartition N → SymmetricFunctions.NPartition N → Prop

Body:
fun {N} mu lam => ∀ (i : Fin N), mu.parts i ≤ lam.parts i

Docstring: Containment of partitions: μ ⊆ λ means μᵢ ≤ λᵢ for all i 

## PROJECT DEPENDENCY SymmetricFunctions.isSSYTFilling (def)
{N : ℕ} → (s : SymmetricFunctions.SkewPartition N) → SymmetricFunctions.SkewFilling s → Prop

Body:
fun {N} s f => SymmetricFunctions.isRowWeak s f ∧ SymmetricFunctions.isColStrict s f

Docstring: Combined predicate for SSYT conditions. 

## PROJECT DEPENDENCY SymmetricFunctions.isSSYTFilling_decidable (def)
{N : ℕ} →
  (s : SymmetricFunctions.SkewPartition N) →
    (f : SymmetricFunctions.SkewFilling s) → Decidable (SymmetricFunctions.isSSYTFilling s f)

Body:
fun {N} s f => instDecidableAnd

Docstring: The SSYT predicate is decidable. 

## PROJECT DEPENDENCY SymmetricFunctions.skewFilling_fintype (def)
{N : ℕ} → (s : SymmetricFunctions.SkewPartition N) → Fintype (SymmetricFunctions.SkewFilling s)

Body:
fun {N} s => inferInstance

Docstring: The type of fillings of a skew shape is finite. 

## PROJECT DEPENDENCY SymmetricFunctions.SkewSSYT.mk (constructor)
{N : ℕ} →
  {s : SymmetricFunctions.SkewPartition N} →
    (entries : (i : Fin N) → Fin (s.outer.parts i - s.inner.parts i) → Fin N) →
      (∀ (i : Fin N) (j k : Fin (s.outer.parts i - s.inner.parts i)), j ≤ k → entries i j ≤ entries i k) →
        (∀ (i : Fin N) (hi : ↑i + 1 < N) (k : Fin (s.outer.parts i - s.inner.parts i)),
            s.inner.parts i + ↑k + 1 > s.inner.parts ⟨↑i + 1, hi⟩ ∧
                s.inner.parts i + ↑k + 1 ≤ s.outer.parts ⟨↑i + 1, hi⟩ →
              let k' := s.inner.parts i + ↑k - s.inner.parts ⟨↑i + 1, hi⟩;
              ∀ (hk' : k' < s.outer.parts ⟨↑i + 1, hi⟩ - s.inner.parts ⟨↑i + 1, hi⟩),
                entries i k < entries ⟨↑i + 1, hi⟩ ⟨k', hk'⟩) →
          SymmetricFunctions.SkewSSYT s

## PROJECT DEPENDENCY SymmetricFunctions.isRowWeak (def)
{N : ℕ} → (s : SymmetricFunctions.SkewPartition N) → SymmetricFunctions.SkewFilling s → Prop

Body:
fun {N} s f => ∀ (i : Fin N) (j k : Fin (s.outer.parts i - s.inner.parts i)), j ≤ k → f i j ≤ f i k

Docstring: Predicate for a filling satisfying the SSYT row-weak condition. 

## PROJECT DEPENDENCY SymmetricFunctions.isColStrict (def)
{N : ℕ} → (s : SymmetricFunctions.SkewPartition N) → SymmetricFunctions.SkewFilling s → Prop

Body:
fun {N} s f =>
  ∀ (i : Fin N) (hi : ↑i + 1 < N) (k : Fin (s.outer.parts i - s.inner.parts i)),
    s.inner.parts i + ↑k + 1 > s.inner.parts ⟨↑i + 1, hi⟩ ∧ s.inner.parts i + ↑k + 1 ≤ s.outer.parts ⟨↑i + 1, hi⟩ →
      have k' := s.inner.parts i + ↑k - s.inner.parts ⟨↑i + 1, hi⟩;
      ∀ (hk' : k' < s.outer.parts ⟨↑i + 1, hi⟩ - s.inner.parts ⟨↑i + 1, hi⟩), f i k < f ⟨↑i + 1, hi⟩ ⟨k', hk'⟩

Docstring: Predicate for a filling satisfying the SSYT column-strict condition.
This is a simplified version that checks the condition for adjacent rows. 

## PROJECT DEPENDENCY SymmetricFunctions.isRowWeak_decidable (def)
{N : ℕ} →
  (s : SymmetricFunctions.SkewPartition N) →
    (f : SymmetricFunctions.SkewFilling s) → Decidable (SymmetricFunctions.isRowWeak s f)

Body:
fun {N} s f => Fintype.decidableForallFintype

Docstring: The row-weak predicate is decidable. 

## PROJECT DEPENDENCY SymmetricFunctions.isColStrict_decidable (def)
{N : ℕ} →
  (s : SymmetricFunctions.SkewPartition N) →
    (f : SymmetricFunctions.SkewFilling s) → Decidable (SymmetricFunctions.isColStrict s f)

Body:
fun {N} s f => Fintype.decidableForallFintype

Docstring: The column-strict predicate is decidable. 

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
thm.sf.skew-schur-symm-jt

\leanhelper  Skew Schur polynomials are symmetric: for any partitions $\lambda \supseteq \mu $, $s_{\lambda /\mu }$ is a symmetric polynomial. 

This provides a proof of symmetry via the Jacobi–Trudi formula, without relying on the Bender–Knuth involution.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.wcomps
def.fps.wcomps

\textbf{(a)} An \emph{(integer) weak composition} means a (finite) tuple of nonnegative integers. \medskip 

\textbf{(b)} The \emph{size} of a weak composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $\alpha _{1}+\alpha _{2}+\cdots +\alpha _{m}$. It is written $\left\vert \alpha \right\vert $. \medskip 

\textbf{(c)} The \emph{length} of a weak composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $m$. It is written $\ell \left( \alpha \right) $. \medskip 

\textbf{(d)} Let $n\in \mathbb {N}$. A \emph{weak composition of }$n$ means a weak composition whose size is $n$. \medskip 

\textbf{(e)} Let $n\in \mathbb {N}$ and $k\in \mathbb {N}$. A \emph{weak composition of }$n$\emph{ into }$k$\emph{ parts} is a weak composition whose size is $n$ and whose length is $k$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-diag
def.sf.skew-diag

Let $\lambda $ and $\mu $ be two $N$-partitions such that $\mu \subseteq \lambda $. Then, we define the \emph{skew Young diagram} $Y\left( \lambda /\mu \right) $ to be the set difference

\begin{align*}  Y\left( \lambda \right) \setminus Y\left( \mu \right) &  =\left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \left[ \lambda _{i}\right] \setminus \left[ \mu _{i}\right] \right\}  \\ &  =\left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \mathbb {Z}\text{ and }\mu _{i}<j\leq \lambda _{i}\right\}  . \end{align*}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-schur
def.sf.skew-schur

Let $\lambda $ and $\mu $ be two $N$-partitions. We define the \emph{skew Schur polynomial} $s_{\lambda /\mu }\in \mathcal{P}$ by

\[  s_{\lambda /\mu }:=\sum _{T\in \operatorname *{SSYT}\left( \lambda /\mu \right) }x_{T}.  \]

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ydiag
def.sf.ydiag

Let $\lambda $ be an $N$-partition. 

The \emph{Young diagram} of $\lambda $ is defined as the set

\[  \left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \left[ \lambda _{i}\right] \right\}  \subseteq \left\{  1,2,3,\ldots \right\}  ^{2}.  \]

 We visually represent each element $\left( i,j\right) $ of this Young diagram as a box in row $i$ and column $j$. 

We denote the Young diagram of $\lambda $ by $Y\left( \lambda \right) $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ytab.skew-xt
def.sf.ytab.skew-xT

Let $\lambda $ and $\mu $ be two $N$-partitions. If $T$ is any Young tableau of shape $\lambda /\mu $, then we define the corresponding monomial

\[  x_{T}:=\prod _{c\text{ is a box of }Y\left( \lambda /\mu \right) }x_{T\left( c\right) }=\prod _{\left( i,j\right) \in Y\left( \lambda /\mu \right) }x_{T\left( i,j\right) }=\prod _{k=1}^{N}x_{k}^{\left( \text{\#  of times }k\text{ appears in }T\right) }.  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint says: \u201cfor any partitions \u03bb \u2287 \u03bc, s_{\u03bb/\u03bc} is a symmetric polynomial.\u201d The formal binders exactly encode two N-partitions and containment: `lam mu : Fin N \u2192 \u2115`, `hlam` and `hmu` require weak decrease, and `hcontained : \u2200 i, mu i \u2264 lam i` matches `\u03bc \u2286 \u03bb`. The conclusion `(SymmetricFunctions.skewSchur ...).IsSymmetric` uses `skewSchur`, whose body is the sum of `T.toMonomial` over all skew SSYTs, and `MvPolynomial.IsSymmetric`, meaning invariance under permutations of variables, matching the informal definitions. The binder `[CommRing R]` is the coefficient-ring setting required by the project\u2019s polynomial and skew-Schur definitions, not an unrelated added hypothesis. Quantification over arbitrary `N` and arbitrary commutative coefficient ring is at least as general as the blueprint\u2019s fixed `N` and `K`. The Jacobi\u2013Trudi wording describes the proof route rather than adding a separate mathematical conclusion to the theorem statement."
}