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

## BASE-LIBRARY REF Matrix
Type u → Type u' → Type v → Type (max u u' v)

Body:
fun m n α => m → n → α

Docstring: `Matrix m n R` is the type of matrices with entries in `R`, whose rows are indexed by `m`
and whose columns are indexed by `n`. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Add
Type u → Type u

Docstring: The homogeneous version of `HAdd`: `a + b : α` where `a b : α`. 

## BASE-LIBRARY REF Add.add
{α : Type u} → [self : Add α] → α → α → α

Body:
fun α [self : Add α] => self.1

Docstring: `a + b` computes the sum of `a` and `b`. See `HAdd`. 

## BASE-LIBRARY REF Nat.add
ℕ → ℕ → ℕ

Body:
fun x x_1 =>
  Nat.brecOn (motive := fun x => ℕ → ℕ) x_1
    (fun x f x_2 =>
      (match (motive := ℕ → (x : ℕ) → Nat.below (motive := fun x => ℕ → ℕ) x → ℕ) x_2, x with
        | a, Nat.zero => fun x => a
        | a, b.succ => fun x => (x.1 a).succ)
        f)
    x

Docstring: Addition of natural numbers, typically used via the `+` operator.

This function is overridden in both the kernel and the compiler to efficiently evaluate using the
arbitrary-precision arithmetic library. The definition provided here is the logical model.


## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Body:
fun n self => self.1

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## BASE-LIBRARY REF Mul
Type u → Type u

Docstring: The homogeneous version of `HMul`: `a * b : α` where `a b : α`. 

## BASE-LIBRARY REF Mul.mul
{α : Type u} → [self : Mul α] → α → α → α

Body:
fun α [self : Mul α] => self.1

Docstring: `a * b` computes the product of `a` and `b`. See `HMul`. 

## BASE-LIBRARY REF Distrib
Type u_1 → Type u_1

Docstring: A typeclass stating that multiplication is left and right distributive
over addition. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring
Type u → Type u

Docstring: A not-necessarily-unital, not-necessarily-associative semiring. See `CommutatorRing` and the
documentation thereof in case you need a `NonUnitalNonAssocSemiring` instance on a Lie ring
or a Lie algebra. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.left_distrib
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a b c : α), a * (b + c) = a * b + a * c

Docstring: Multiplication is left distributive over addition 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.right_distrib
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a b c : α), (a + b) * c = a * c + b * c

Docstring: Multiplication is right distributive over addition 

## BASE-LIBRARY REF NonUnitalNonAssocRing
Type u → Type u

Docstring: A not-necessarily-unital, not-necessarily-associative ring. 

## BASE-LIBRARY REF AddCommGroup.add_comm
∀ {G : Type u} [self : AddCommGroup G] (a b : G), a + b = b + a

Docstring: Addition is commutative in a commutative additive magma. 

## BASE-LIBRARY REF NonUnitalNonAssocRing.left_distrib
∀ {α : Type u} [self : NonUnitalNonAssocRing α] (a b c : α), a * (b + c) = a * b + a * c

Docstring: Multiplication is left distributive over addition 

## BASE-LIBRARY REF NonUnitalNonAssocRing.right_distrib
∀ {α : Type u} [self : NonUnitalNonAssocRing α] (a b c : α), (a + b) * c = a * c + b * c

Docstring: Multiplication is right distributive over addition 

## BASE-LIBRARY REF NonUnitalNonAssocRing.zero_mul
∀ {α : Type u} [self : NonUnitalNonAssocRing α] (a : α), 0 * a = 0

Docstring: Zero is a left absorbing element for multiplication 

## BASE-LIBRARY REF NonUnitalNonAssocCommRing
Type u → Type u

Docstring: A non-unital non-associative commutative ring is a `NonUnitalNonAssocRing` with commutative
multiplication. 

## BASE-LIBRARY REF NonUnitalCommRing
Type u → Type u

Docstring: A non-unital commutative ring is a `NonUnitalRing` with commutative multiplication. 

## BASE-LIBRARY REF NonUnitalCommRing.mul_comm
∀ {α : Type u} [self : NonUnitalCommRing α] (a b : α), a * b = b * a

Docstring: Multiplication is commutative in a commutative multiplicative magma. 

## BASE-LIBRARY REF Matrix.det
{n : Type u_2} → [DecidableEq n] → [Fintype n] → {R : Type v} → [CommRing R] → Matrix n n R → R

Body:
fun {n} [DecidableEq n] [Fintype n] {R} [CommRing R] M => Matrix.detRowAlternating M

Docstring: The determinant of a matrix given by the Leibniz formula. 

## BASE-LIBRARY REF instDecidableEqFin.match_1
(n : ℕ) →
  (i j : Fin n) →
    (motive : Decidable (↑i = ↑j) → Sort u_1) →
      (x : Decidable (↑i = ↑j)) → ((h : ↑i = ↑j) → motive (isTrue h)) → ((h : ¬↑i = ↑j) → motive (isFalse h)) → motive x

Body:
fun n i j motive x h_1 h_2 => Decidable.casesOn x (fun h => h_2 h) fun h => h_1 h

## BASE-LIBRARY REF decEq
{α : Sort u} → [inst : DecidableEq α] → (a b : α) → Decidable (a = b)

Body:
fun {α} [inst : DecidableEq α] a b => inst a b

Docstring: Checks whether two terms of a type are equal using the type's `DecidableEq` instance.


## BASE-LIBRARY REF Decidable.isTrue
{p : Prop} → p → Decidable p

Docstring: Proves that `p` is decidable by supplying a proof of `p` 

## BASE-LIBRARY REF Fin.eq_of_val_eq
∀ {n : ℕ} {i j : Fin n}, ↑i = ↑j → i = j

## BASE-LIBRARY REF Decidable.isFalse
{p : Prop} → ¬p → Decidable p

Docstring: Proves that `p` is decidable by supplying a proof of `¬p` 

## BASE-LIBRARY REF instDecidableEqFin._proof_1
∀ (n : ℕ) (i j : Fin n), ¬↑i = ↑j → i = j → False

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

Body:
fun n => { elems := { val := ↑(List.finRange n), nodup := ⋯ }, complete := ⋯ }

## BASE-LIBRARY REF Multiset.ofList
{α : Type u_1} → List α → Multiset α

Body:
fun {α} => Quot.mk ⇑(List.isSetoid α)

Docstring: The quotient map from `List α` to `Multiset α`. 

## BASE-LIBRARY REF List.finRange
(n : ℕ) → List (Fin n)

Body:
fun n => List.ofFn fun i => i

Docstring: Lists all elements of `Fin n` in order, starting at `0`.

Examples:
* `List.finRange 0 = ([] : List (Fin 0))`
* `List.finRange 2 = ([0, 1] : List (Fin 2))`


## BASE-LIBRARY REF List.nodup_finRange
∀ (n : ℕ), (List.finRange n).Nodup

## BASE-LIBRARY REF List.mem_finRange
∀ {n : ℕ} (x : Fin n), x ∈ List.finRange n

## BASE-LIBRARY REF Sub
Type u → Type u

Docstring: The homogeneous version of `HSub`: `a - b : α` where `a b : α`. 

## BASE-LIBRARY REF Sub.sub
{α : Type u} → [self : Sub α] → α → α → α

Body:
fun α [self : Sub α] => self.1

Docstring: `a - b` computes the difference of `a` and `b`. See `HSub`. 

## BASE-LIBRARY REF SubNegMonoid
Type u → Type u

Docstring: A `SubNegMonoid` is an `AddMonoid` with unary `-` and binary `-` operations
satisfying `sub_eq_add_neg : ∀ a b, a - b = a + -b`.

The default for `sub` is such that `a - b = a + -b` holds by definition.

Adding `sub` as a field rather than defining `a - b := a + -b` allows us to
avoid certain classes of unification failures, for example:
Let `foo X` be a type with a `∀ X, Sub (Foo X)` instance but no
`∀ X, Neg (Foo X)`. Suppose we also have an instance
`∀ X [Cromulent X], AddGroup (Foo X)`. Then the `(-)` coming from
`AddGroup.sub` cannot be definitionally equal to the `(-)` coming from
`Foo.Sub`.

In the same way, adding a `zsmul` field makes it possible to avoid definitional failures
in diamonds. See the definition of `AddMonoid` and Note [forgetful inheritance] for more
explanations on this.


## BASE-LIBRARY REF AddGroupWithOne
Type u → Type u

Docstring: An `AddGroupWithOne` is an `AddGroup` with a 1. It also contains data for the unique
homomorphisms `ℕ → R` and `ℤ → R`. 

## BASE-LIBRARY REF AddGroupWithOne.neg_add_cancel
∀ {R : Type u} [self : AddGroupWithOne R] (a : R), -a + a = 0

## BASE-LIBRARY REF Ring
Type u → Type u

Docstring: A `Ring` is a `Semiring` with negation making it an additive group. 

## BASE-LIBRARY REF Matrix.submatrix
{l : Type u_1} →
  {m : Type u_2} → {n : Type u_3} → {o : Type u_4} → {α : Type v} → Matrix m n α → (l → m) → (o → n) → Matrix l o α

Body:
fun {l} {m} {n} {o} {α} A r c => Matrix.of fun i j => A (r i) (c j)

Docstring: Given maps `(r : l → m)` and `(c : o → n)` reindexing the rows and columns of
a matrix `M : Matrix m n α`, the matrix `M.submatrix r c : Matrix l o α` is defined
by `(M.submatrix r c) i j = M (r i) (c j)` for `(i,j) : l × o`.
Note that the total number of row and columns does not have to be preserved. 

## BASE-LIBRARY REF Fin.succAbove
{n : ℕ} → Fin (n + 1) → Fin n → Fin (n + 1)

Body:
fun {n} p i => if i.castSucc < p then i.castSucc else i.succ

Docstring: `succAbove p i` embeds `Fin n` into `Fin (n + 1)` with a hole around `p`. 

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Body:
fun {α} c [h : Decidable c] t e => Decidable.casesOn h (fun x => e) fun x => t

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF Nat.decLt
(n m : ℕ) → Decidable (n < m)

Body:
fun n m => n.succ.decLe m

Docstring: A decision procedure for strict inequality of natural numbers, usually accessed via the
`DecidableLT Nat` instance.

Examples:
 * `(if 3 < 4 then "yes" else "no") = "yes"`
 * `(if 4 < 4 then "yes" else "no") = "no"`
 * `(if 6 < 4 then "yes" else "no") = "no"`
 * `show 5 < 12 by decide`


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
  "verdict": "faithful",
  "discrepancies": [],
  "justification": "The formal theorem exactly matches the identity. Writing the informal size as `n = m + 2` covers precisely every `n \u2265 2`; the indices `p q u v : Fin (m + 2)` represent elements of `[n]`, with the same hypotheses `p < q` and `u < v`. Unfolding `submatrixRemove2` gives `A.submatrix (p.skipTwo q hpq) (u.skipTwo v huv)`, which removes rows `p,q` and columns `u,v`, while unfolding `submatrixRemove A i j` gives `A.submatrix i.succAbove j.succAbove`, removing row `i` and column `j`. Thus the four one-row/one-column minors and the two-row/two-column minor occur in exactly the positions stated informally. The binder `[CommRing R]` supplies the coefficient setting required by the formal determinant and does not restrict any coefficient domain fixed by the blueprint."
}