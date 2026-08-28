## TARGET AlgebraicCombinatorics.CauchyBinet.det_const_add_diagonal (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommRing R] {n : ℕ} (x : R) (d : Fin n → R),
  (AlgebraicCombinatorics.CauchyBinet.constPlusDiagMatrix x d).det = ∏ i, d i + x * ∑ i, ∏ j ∈ Finset.univ.erase i, d j

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.constPlusDiagMatrix (def)
{R : Type u_1} → [CommRing R] → {n : ℕ} → R → (Fin n → R) → Matrix (Fin n) (Fin n) R

Body:
fun {R} [CommRing R] {n} x d i j => x + if i = j then d i else 0

Docstring: The matrix with x on all entries except diagonal which has x + dᵢ.
(Used in Proposition prop.det.x+ai) 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


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

## BASE-LIBRARY REF Matrix.det
{n : Type u_2} → [DecidableEq n] → [Fintype n] → {R : Type v} → [CommRing R] → Matrix n n R → R

Docstring: The determinant of a matrix given by the Leibniz formula. 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

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

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toDistrib
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → Distrib α

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF CommRing.toCommMonoid
{α : Type u} → [self : CommRing α] → CommMonoid α

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF Distrib.toMul
{R : Type u_1} → [self : Distrib R] → Mul R

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toAddCommMonoid
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → AddCommMonoid α

## BASE-LIBRARY REF Finset.erase
{α : Type u_1} → [DecidableEq α] → Finset α → α → Finset α

Docstring: `erase s a` is the set `s - {a}`, that is, the elements of `s` which are
not equal to `a`. 

## INFORMAL STATEMENT
prop.det.x+ai

Let $n\in \mathbb {N}$. Let $d_1,d_2,\ldots ,d_n\in K$ and $x\in K$. Let $F$ be the $n\times n$-matrix 

\[  \begin{pmatrix}  x+d_1 

&  x 

&  \cdots 

&  x

\\ x 

&  x+d_2 

&  \cdots 

&  x

\\ \vdots 

&  \vdots 

&  \ddots 

&  \vdots 

\\ x 

&  x 

&  \cdots 

&  x+d_n 

\end{pmatrix}\in K^{n\times n}.  \]

 Then, 

\[  \det F = d_1 d_2 \cdots d_n + x \sum _{i=1}^n d_1 d_2 \cdots \widehat{d_i} \cdots d_n,  \]

 where the hat over “$d_i$” means “omit the $d_i$ factor.”

## INFORMAL DEPENDENCY stmt-algebraic-combinatorics-lem.constplusdiag.decomp
lem.constPlusDiag.decomp

\leanhelper  The matrix $F$ with entries $F_{i,j} = x + d_i\, [i{=}j]$ decomposes as $F = A + D$ where $A$ is the $n\times n$ constant matrix with all entries equal to~ $x$ and $D = \operatorname {diag}(d_1,\ldots ,d_n)$.

## INFORMAL DEPENDENCY stmt-algebraic-combinatorics-lem.det.const.matrix.zero
lem.det.const.matrix.zero

\leanhelper  Let $A$ be the $n\times n$ constant matrix with all entries equal to $x$. If $P\subseteq [n]$ has $|P| \ge 2$, then $\det (\operatorname {sub}_P^P A) = 0$.

## INFORMAL DEPENDENCY stmt-algebraic-combinatorics-thm.det.det-a-d-
thm.det.det(A+D)

Let $n\in \mathbb {N}$. Let $A$ and $D$ be two $n\times n$-matrices in $K^{n\times n}$ such that the matrix $D$ is diagonal. Let $d_1,d_2,\ldots ,d_n$ be the diagonal entries of the diagonal matrix $D$. Then, 

\[  \det (A+D) = \sum _{P\subseteq [n]} \det (\operatorname {sub}_P^P A) \cdot \prod _{i\in [n]\setminus P} d_i.  \]

 The minors $\det (\operatorname {sub}_P^P A)$ are called the \emph{principal minors} of $A$.

## VERDICT
{
  "verdict": "unclear",
  "justification": "The matrix and formula otherwise match exactly: `constPlusDiagMatrix x d ... => x + if i = j then d i else 0` gives diagonal entries `x+d\u1d62` and off-diagonal entries `x`, while `\u220f i, d i + x * \u2211 i, \u220f j \u2208 Finset.univ.erase i, d j` is precisely the full product plus `x` times the sum of products omitting one factor. The missing information is the algebraic status and quantification of `K` in the informal statement (`d_1,...,d_n \u2208 K` and `F \u2208 K^{n\u00d7n}`). The Lean declaration quantifies over every `{R : Type} [CommRing R]`. If `K` is intended to range over arbitrary commutative rings, the formalization is faithful. If `K` is an ambient field or a fixed coefficient structure, Lean makes a broader claim, so the informal statement does not imply the Lean statement. The package would need the source convention or declaration specifying what `K` denotes and how it is quantified."
}