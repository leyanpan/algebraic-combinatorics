## TARGET AlgebraicCombinatorics.Determinants.desnanot_jacobi_base (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommRing R] (A : Matrix (Fin 2) (Fin 2) R),
  A.det * (AlgebraicCombinatorics.Determinants.innerSubmatrix A).det =
    (AlgebraicCombinatorics.Determinants.submatrixRemove A 0 0).det *
        (AlgebraicCombinatorics.Determinants.submatrixRemove A (Fin.last 1) (Fin.last 1)).det -
      (AlgebraicCombinatorics.Determinants.submatrixRemove A 0 (Fin.last 1)).det *
        (AlgebraicCombinatorics.Determinants.submatrixRemove A (Fin.last 1) 0).det

Docstring: Desnanot-Jacobi identity for 2×2 matrices (base case) 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Determinants.innerSubmatrix (def)
{R : Type u_1} → {m : ℕ} → Matrix (Fin (m + 2)) (Fin (m + 2)) R → Matrix (Fin m) (Fin m) R

Body:
fun {R} {m} A => A.submatrix (fun i => i.succ.castSucc) fun j => j.succ.castSucc

Docstring: The inner submatrix A' in the Desnanot-Jacobi identity:
the (n-2)×(n-2) matrix obtained by removing first/last rows and columns.
Label: thm.det.des-jac-1 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Determinants.submatrixRemove (def)
{R : Type u_1} → {m : ℕ} → Matrix (Fin (m + 1)) (Fin (m + 1)) R → Fin (m + 1) → Fin (m + 1) → Matrix (Fin m) (Fin m) R

Body:
fun {R} {m} A i j => A.submatrix i.succAbove j.succAbove

Docstring: Convention conv.mat.tilde: A_{~i,~j} denotes the submatrix obtained by
removing row i and column j.

In Mathlib, this is `Matrix.submatrix A (Fin.succAbove i) (Fin.succAbove j)`
for an (n+1)×(n+1) matrix A, yielding an n×n matrix. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Matrix
Type u → Type u' → Type v → Type (max u u' v)

Docstring: `Matrix m n R` is the type of matrices with entries in `R`, whose rows are indexed by `m`
and whose columns are indexed by `n`. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

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

## BASE-LIBRARY REF Matrix.det
{n : Type u_2} → [DecidableEq n] → [Fintype n] → {R : Type v} → [CommRing R] → Matrix n n R → R

Docstring: The determinant of a matrix given by the Leibniz formula. 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF SubNegMonoid.toSub
{G : Type u} → [self : SubNegMonoid G] → Sub G

## BASE-LIBRARY REF AddGroup.toSubNegMonoid
{A : Type u} → [self : AddGroup A] → SubNegMonoid A

## BASE-LIBRARY REF AddGroupWithOne.toAddGroup
{R : Type u} → [self : AddGroupWithOne R] → AddGroup R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF CommRing.toRing
{α : Type u} → [self : CommRing α] → Ring α

## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF instAddNat
Add ℕ

## BASE-LIBRARY REF Fin.instOfNat
{n : ℕ} → [NeZero n] → {i : ℕ} → OfNat (Fin n) i

## BASE-LIBRARY REF instNeZeroNatHAdd_1
∀ {n m : ℕ} [h : NeZero m], NeZero (n + m)

## BASE-LIBRARY REF Nat.instNeZeroSucc
∀ {n : ℕ}, NeZero (n + 1)

## BASE-LIBRARY REF Fin.last
(n : ℕ) → Fin (n + 1)

Docstring: The greatest value of `Fin (n+1)`, namely `n`.

Examples:
* `Fin.last 4 = (4 : Fin 5)`
* `(Fin.last 0).val = (0 : Nat)`


## BASE-LIBRARY REF Matrix.submatrix
{l : Type u_1} →
  {m : Type u_2} → {n : Type u_3} → {o : Type u_4} → {α : Type v} → Matrix m n α → (l → m) → (o → n) → Matrix l o α

Docstring: Given maps `(r : l → m)` and `(c : o → n)` reindexing the rows and columns of
a matrix `M : Matrix m n α`, the matrix `M.submatrix r c : Matrix l o α` is defined
by `(M.submatrix r c) i j = M (r i) (c j)` for `(i,j) : l × o`.
Note that the total number of row and columns does not have to be preserved. 

## BASE-LIBRARY REF Fin.castSucc
{n : ℕ} → Fin n → Fin (n + 1)

Docstring: Coarsens a bound by one.


## BASE-LIBRARY REF Fin.succ
{n : ℕ} → Fin n → Fin (n + 1)

Docstring: The successor, with an increased bound.

This differs from adding `1`, which instead wraps around.

Examples:
* `(2 : Fin 3).succ = (3 : Fin 4)`
* `(2 : Fin 3) + 1 = (0 : Fin 3)`


## BASE-LIBRARY REF Fin.succAbove
{n : ℕ} → Fin (n + 1) → Fin n → Fin (n + 1)

Docstring: `succAbove p i` embeds `Fin n` into `Fin (n + 1)` with a hole around `p`. 

## INFORMAL STATEMENT
lem.det.desnanot-jacobi-base

\leanhelper  The Desnanot–Jacobi identity holds for $2 \times 2$ matrices by direct computation.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint says, \u201cThe Desnanot\u2013Jacobi identity holds for 2 \u00d7 2 matrices by direct computation.\u201d The target quantifies exactly over `A : Matrix (Fin 2) (Fin 2) R` and states the Desnanot\u2013Jacobi equality using the defined inner minor and four row/column-deletion minors. By the dependency bodies, `innerSubmatrix A` removes the first and last rows and columns, while `submatrixRemove A i j` removes row `i` and column `j`; `0` and `Fin.last 1` are precisely the two indices of `Fin 2`. The binder `[CommRing R]` is the algebraic setting required by `Matrix.det` and supports the stated determinant identity; it does not narrow any coefficient setting fixed by the informal statement. Thus the formal theorem faithfully gives the claimed 2\u00d72 base case."
}