## TARGET AlgebraicCombinatorics.CauchyBinet.det_diagonal_submatrix_off_diag (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommRing R] {n : ℕ} (d : Fin n → R) (P Q : Finset (Fin n)) (hcard : P.card = Q.card),
  P ≠ Q → ((Matrix.diagonal d).submatrix ⇑(P.orderEmbOfFin ⋯) ⇑(Q.orderEmbOfFin ⋯)).det = 0

Docstring: Part (b): Off-diagonal submatrices of a diagonal matrix have zero determinant.
(Lemma lem.det.minors-diag (b))
Label: lem.det.minors-diag.b 

## TARGET AlgebraicCombinatorics.CauchyBinet.det_diagonal_submatrix_eq (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommRing R] {n : ℕ} (d : Fin n → R) (P : Finset (Fin n)),
  ((Matrix.diagonal d).submatrix ⇑(P.orderEmbOfFin ⋯) ⇑(P.orderEmbOfFin ⋯)).det = ∏ i ∈ P, d i

Docstring: Part (a): Principal minors of a diagonal matrix are products of diagonal entries.
(Lemma lem.det.minors-diag (a))
Label: lem.det.minors-diag.a 

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


## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

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

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

## BASE-LIBRARY REF Matrix.det
{n : Type u_2} → [DecidableEq n] → [Fintype n] → {R : Type v} → [CommRing R] → Matrix n n R → R

Docstring: The determinant of a matrix given by the Leibniz formula. 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Matrix.submatrix
{l : Type u_1} →
  {m : Type u_2} → {n : Type u_3} → {o : Type u_4} → {α : Type v} → Matrix m n α → (l → m) → (o → n) → Matrix l o α

Docstring: Given maps `(r : l → m)` and `(c : o → n)` reindexing the rows and columns of
a matrix `M : Matrix m n α`, the matrix `M.submatrix r c : Matrix l o α` is defined
by `(M.submatrix r c) i j = M (r i) (c j)` for `(i,j) : l × o`.
Note that the total number of row and columns does not have to be preserved. 

## BASE-LIBRARY REF Matrix.diagonal
{n : Type u_3} → {α : Type v} → [DecidableEq n] → [Zero α] → (n → α) → Matrix n n α

Docstring: `diagonal d` is the square matrix such that `(diagonal d) i i = d i` and `(diagonal d) i j = 0`
if `i ≠ j`.

Note that bundled versions exist as:
* `Matrix.diagonalAddMonoidHom`
* `Matrix.diagonalLinearMap`
* `Matrix.diagonalRingHom`
* `Matrix.diagonalAlgHom`


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

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF OrderEmbedding
(α : Type u_6) → (β : Type u_7) → [LE α] → [LE β] → Type (max u_6 u_7)

Docstring: An order embedding is an embedding `f : α ↪ β` such that `a ≤ b ↔ (f a) ≤ (f b)`.
This definition is an abbreviation of `RelEmbedding (≤) (≤)`. 

## BASE-LIBRARY REF instLEFin
{n : ℕ} → LE (Fin n)

## BASE-LIBRARY REF Preorder.toLE
{α : Type u_2} → [self : Preorder α] → LE α

## BASE-LIBRARY REF PartialOrder.toPreorder
{α : Type u_2} → [self : PartialOrder α] → Preorder α

## BASE-LIBRARY REF SemilatticeInf.toPartialOrder
{α : Type u} → [self : SemilatticeInf α] → PartialOrder α

## BASE-LIBRARY REF Lattice.toSemilatticeInf
{α : Type u} → [self : Lattice α] → SemilatticeInf α

## BASE-LIBRARY REF DistribLattice.toLattice
{α : Type u_1} → [self : DistribLattice α] → Lattice α

## BASE-LIBRARY REF instDistribLatticeOfLinearOrder
{α : Type u} → [LinearOrder α] → DistribLattice α

## BASE-LIBRARY REF Fin.instLinearOrder
{n : ℕ} → LinearOrder (Fin n)

## BASE-LIBRARY REF instFunLikeOrderEmbedding
(α : Type u_6) → (β : Type u_7) → [inst : LE α] → [inst_1 : LE β] → FunLike (α ↪o β) α β

## BASE-LIBRARY REF Finset.orderEmbOfFin
{α : Type u_1} → [inst : LinearOrder α] → (s : Finset α) → {k : ℕ} → s.card = k → Fin k ↪o α

Docstring: Given a finset `s` of cardinality `k` in a linear order `α`, the map `orderEmbOfFin s h` is
the increasing bijection between `Fin k` and `s` as an order embedding into `α`. Here, `h` is a
proof that the cardinality of `s` is `k`. We use this instead of an embedding `Fin s.card ↪o α` to
avoid casting issues in further uses of this function. 

## BASE-LIBRARY REF rfl
∀ {α : Sort u} {a : α}, a = a

Docstring: `rfl : a = a` is the unique constructor of the equality type. This is the
same as `Eq.refl` except that it takes `a` implicitly instead of explicitly.

This is a more powerful theorem than it may appear at first, because although
the statement of the theorem is `a = a`, Lean will allow anything that is
definitionally equal to that type. So, for instance, `2 + 2 = 4` is proven in
Lean by `rfl`, because both sides are the same up to definitional equality.


## BASE-LIBRARY REF Eq.rec
{α : Sort u_1} →
  {a : α} → {motive : (a_1 : α) → a = a_1 → Sort u} → motive a ⋯ → {a_1 : α} → (t : a = a_1) → motive a_1 t

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF CommRing.toCommMonoid
{α : Type u} → [self : CommRing α] → CommMonoid α

## INFORMAL STATEMENT
lem.det.minors-diag

Let $n\in \mathbb {N}$. Let $d_1,d_2,\ldots ,d_n\in K$. Let 

\[  D:=\operatorname {diag}(d_1,d_2,\ldots ,d_n) =\begin{pmatrix}  d_1 

&  0 

&  \cdots 

&  0

\\ 0 

&  d_2 

&  \cdots 

&  0

\\ \vdots 

&  \vdots 

&  \ddots 

&  \vdots 

\\ 0 

&  0 

&  \cdots 

&  d_n 

\end{pmatrix}\in K^{n\times n}.  \]

\textbf{(a)} We have $\det (\operatorname {sub}_P^P D) = \prod _{i\in P} d_i$ for any subset $P$ of $[n]$. 

\textbf{(b)} Let $P$ and $Q$ be two distinct subsets of $[n]$ satisfying $|P|=|Q|$. Then, $\det (\operatorname {sub}_P^Q D) = 0$.

## VERDICT
{
  "verdict": "unclear",
  "justification": "The informal statement only says \u201cd\u2081,\u2026,d\u2099 \u2208 K\u201d and does not specify the algebraic structure on K, while both elaborated targets add the binder \u201c{R : Type u_1} [inst : CommRing R]\u201d. The package contains no informal definition or other standard-setting declaration identifying K as a field, commutative ring, or another structure. Thus it is impossible to determine whether `[CommRing R]` is a harmless generalization/encoding or a contentful added restriction. If K is intended to be a field or commutative ring, both targets faithfully express parts (a) and (b), with the formal statements even covering every commutative ring; `Fin n` merely reindexes `[n]`. If K is intended more generally, the `CommRing` binder may be drift. The package would need the blueprint\u2019s definition or ambient assumption for K to decide."
}