## TARGET AlgebraicCombinatorics.Determinants.desnanot_jacobi_general (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommRing R] {m : ℕ} (A : Matrix (Fin (m + 2)) (Fin (m + 2)) R) (p q u v : Fin (m + 2))
  (hpq : p < q) (huv : u < v),
  A.det * (AlgebraicCombinatorics.Determinants.submatrixRemove2 A p q u v hpq huv).det =
    (AlgebraicCombinatorics.Determinants.submatrixRemove A p u).det *
        (AlgebraicCombinatorics.Determinants.submatrixRemove A q v).det -
      (AlgebraicCombinatorics.Determinants.submatrixRemove A p v).det *
        (AlgebraicCombinatorics.Determinants.submatrixRemove A q u).det

Docstring: Generalized Desnanot-Jacobi identity (Theorem thm.det.des-jac-2):
For p < q and u < v,
det(A) · det(sub_{[n]\{p,q}}^{[n]\{u,v}} A) =
  det(A_{~p,~u}) · det(A_{~q,~v}) - det(A_{~p,~v}) · det(A_{~q,~u})

The proof follows from Jacobi's complementary minor theorem for the 2×2 case.
By comparing the 2×2 determinant of the adjugate submatrix (computed two ways),
we obtain the desired identity.
Label: thm.det.des-jac-2 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Determinants.submatrixRemove2 (def)
{R : Type u_1} →
  {m : ℕ} → Matrix (Fin (m + 2)) (Fin (m + 2)) R → (p q u v : Fin (m + 2)) → p < q → u < v → Matrix (Fin m) (Fin m) R

Body:
fun {R} {m} A p q u v hpq huv => A.submatrix (p.skipTwo q hpq) (u.skipTwo v huv)

Docstring: Submatrix removing two rows (p, q with p < q) and two columns (u, v with u < v).
This is the submatrix sub_{[n]\{p,q}}^{[n]\{u,v}} A in the source notation. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Determinants.submatrixRemove (def)
{R : Type u_1} → {m : ℕ} → Matrix (Fin (m + 1)) (Fin (m + 1)) R → Fin (m + 1) → Fin (m + 1) → Matrix (Fin m) (Fin m) R

Body:
fun {R} {m} A i j => A.submatrix i.succAbove j.succAbove

Docstring: Convention conv.mat.tilde: A_{~i,~j} denotes the submatrix obtained by
removing row i and column j.

In Mathlib, this is `Matrix.submatrix A (Fin.succAbove i) (Fin.succAbove j)`
for an (n+1)×(n+1) matrix A, yielding an n×n matrix. 

## PROJECT DEPENDENCY Fin.skipTwo (def)
{n : ℕ} → (i j : Fin (n + 2)) → i < j → Fin n → Fin (n + 2)

Body:
fun {n} i j _hij k => if ↑k < ↑i then ⟨↑k, ⋯⟩ else if ↑k + 1 < ↑j then ⟨↑k + 1, ⋯⟩ else ⟨↑k + 2, ⋯⟩

Docstring: Remove two elements from `Fin (n+2)` to get `Fin n`.
Given `i < j` in `Fin (n+2)`, we map `Fin n` to `Fin (n+2)` by skipping `i` and `j`.

The function is defined piecewise:
- If `k < i`, then `skipTwo i j k = k`
- If `i ≤ k` and `k + 1 < j`, then `skipTwo i j k = k + 1`
- If `k + 1 ≥ j`, then `skipTwo i j k = k + 2` 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Matrix
Type u → Type u' → Type v → Type (max u u' v)

Docstring: `Matrix m n R` is the type of matrices with entries in `R`, whose rows are indexed by `m`
and whose columns are indexed by `n`. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTFin
{n : ℕ} → LT (Fin n)

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

## BASE-LIBRARY REF Matrix.submatrix
{l : Type u_1} →
  {m : Type u_2} → {n : Type u_3} → {o : Type u_4} → {α : Type v} → Matrix m n α → (l → m) → (o → n) → Matrix l o α

Docstring: Given maps `(r : l → m)` and `(c : o → n)` reindexing the rows and columns of
a matrix `M : Matrix m n α`, the matrix `M.submatrix r c : Matrix l o α` is defined
by `(M.submatrix r c) i j = M (r i) (c j)` for `(i,j) : l × o`.
Note that the total number of row and columns does not have to be preserved. 

## BASE-LIBRARY REF Fin.succAbove
{n : ℕ} → Fin (n + 1) → Fin n → Fin (n + 1)

Docstring: `succAbove p i` embeds `Fin n` into `Fin (n + 1)` with a hole around `p`. 

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## BASE-LIBRARY REF Nat.decLt
(n m : ℕ) → Decidable (n < m)

Docstring: A decision procedure for strict inequality of natural numbers, usually accessed via the
`DecidableLT Nat` instance.

Examples:
 * `(if 3 < 4 then "yes" else "no") = "yes"`
 * `(if 4 < 4 then "yes" else "no") = "no"`
 * `(if 6 < 4 then "yes" else "no") = "no"`
 * `show 5 < 12 by decide`


## BASE-LIBRARY REF Fin.mk
{n : ℕ} → (val : ℕ) → val < n → Fin n

Docstring: Creates a `Fin n` from `i : Nat` and a proof that `i < n`. 

## INFORMAL STATEMENT
thm.det.des-jac-2

Let $n \in \mathbb {N}$ be such that $n \geq 2$. Let $p, q, u, v$ be four elements of $[n]$ such that $p < q$ and $u < v$. Let $A$ be an $n \times n$-matrix. Then, 

\begin{align*} &  \det A \cdot \det \left( \operatorname {sub}_{[n] \setminus \{ p, q\} }^{[n] \setminus \{ u, v\} } A \right) \\ & = \det (A_{\sim p, \sim u}) \cdot \det (A_{\sim q, \sim v}) - \det (A_{\sim p, \sim v}) \cdot \det (A_{\sim q, \sim u}). \end{align*}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-schur
def.sf.skew-schur

Let $\lambda $ and $\mu $ be two $N$-partitions. We define the \emph{skew Schur polynomial} $s_{\lambda /\mu }\in \mathcal{P}$ by

\[  s_{\lambda /\mu }:=\sum _{T\in \operatorname *{SSYT}\left( \lambda /\mu \right) }x_{T}.  \]

## VERDICT
{
  "verdict": "unclear",
  "justification": "The blueprint says only \u201cLet A be an n \u00d7 n-matrix\u201d and does not specify its coefficient type or algebraic assumptions. The Lean declaration quantifies \u201c\u2200 {R : Type u_1} [inst : CommRing R]\u201d and therefore states the identity for matrices over commutative rings. The package contains no informal definition or other standard-setting text fixing what kind of entries the blueprint\u2019s matrices have, and the unrelated skew-Schur definition does not resolve this. Thus it is impossible to determine whether `[CommRing R]` is merely the intended formal setting or a contentful restriction. If the blueprint intends matrices over an arbitrary commutative ring (or a fixed field), the declaration is faithful and possibly more general; otherwise it may drift. The remaining indexing agrees: `m + 2` represents all `n \u2265 2`, `p < q` and `u < v` are preserved, and `submatrixRemove`/`submatrixRemove2` implement the stated deleted-row and deleted-column minors. The package would need the coefficient-domain convention for \u201cmatrix\u201d in the informal statement to decide the verdict."
}