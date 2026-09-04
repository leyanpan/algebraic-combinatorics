## TARGET AlgebraicCombinatorics.Det.det_add_smul_col (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {n : ℕ} (A : Matrix (Fin n) (Fin n) K) (i j : Fin n),
  i ≠ j → ∀ (c : K), (A.updateCol i fun k => A k i + c * A k j).det = A.det

Docstring: (f) Adding λ times one column to another preserves determinant.
Label: thm.det.colop (f) 

## TARGET AlgebraicCombinatorics.Det.det_zero_col (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {n : ℕ} (A : Matrix (Fin n) (Fin n) K) (j : Fin n),
  (∀ (i : Fin n), A i j = 0) → A.det = 0

Docstring: A matrix with a zero column has determinant 0.
Label: thm.det.colop (b) 

## TARGET AlgebraicCombinatorics.Det.det_scale_col (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {n : ℕ} (A : Matrix (Fin n) (Fin n) K) (j : Fin n) (c : K),
  (Matrix.of fun i k => if k = j then c * A i k else A i k).det = c * A.det

Docstring: Scaling a column by λ scales the determinant by λ.
Label: thm.det.colop (d) 

## TARGET AlgebraicCombinatorics.Det.det_swap_cols (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {n : ℕ} (A : Matrix (Fin n) (Fin n) K) (i j : Fin n),
  i ≠ j → (A.submatrix id ⇑(Equiv.swap i j)).det = -A.det

Docstring: (a) Swapping two columns multiplies determinant by -1.
Label: thm.det.colop (a) 

## TARGET AlgebraicCombinatorics.Det.det_add_col (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {n : ℕ} (A : Matrix (Fin n) (Fin n) K) (i j : Fin n),
  i ≠ j → (A.updateCol i fun k => A k i + A k j).det = A.det

Docstring: (e) Adding one column to another preserves determinant (special case of (f)).
Label: thm.det.colop (e) 

## TARGET AlgebraicCombinatorics.Det.det_col_add (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {n : ℕ} (A B C : Matrix (Fin n) (Fin n) K) (k : Fin n),
  (∀ (i : Fin n), C i k = A i k + B i k) →
    (∀ (i j : Fin n), j ≠ k → C i j = A i j ∧ A i j = B i j) → C.det = A.det + B.det

Docstring: (g) Multilinearity: determinant is additive in column k.
Label: thm.det.colop (g) 

## TARGET AlgebraicCombinatorics.Det.det_eq_cols (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {n : ℕ} (A : Matrix (Fin n) (Fin n) K) (i j : Fin n),
  i ≠ j → (∀ (k : Fin n), A k i = A k j) → A.det = 0

Docstring: (c) A matrix with two equal columns has determinant 0.
Label: thm.det.colop (c) 

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

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Body:
fun n self => self.1

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


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

## BASE-LIBRARY REF Matrix.updateCol
{m : Type u_2} → {n : Type u_3} → {α : Type v} → [DecidableEq n] → Matrix m n α → n → (m → α) → Matrix m n α

Body:
fun {m} {n} {α} [DecidableEq n] M j b => Matrix.of fun i => Function.update (M i) j (b i)

Docstring: Update, i.e. replace the `j`th column of matrix `A` with the values in `b`. 

## BASE-LIBRARY REF Add
Type u → Type u

Docstring: The homogeneous version of `HAdd`: `a + b : α` where `a b : α`. 

## BASE-LIBRARY REF Add.add
{α : Type u} → [self : Add α] → α → α → α

Body:
fun α [self : Add α] => self.1

Docstring: `a + b` computes the sum of `a` and `b`. See `HAdd`. 

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

## BASE-LIBRARY REF Mul
Type u → Type u

Docstring: The homogeneous version of `HMul`: `a * b : α` where `a b : α`. 

## BASE-LIBRARY REF Mul.mul
{α : Type u} → [self : Mul α] → α → α → α

Body:
fun α [self : Mul α] => self.1

Docstring: `a * b` computes the product of `a` and `b`. See `HMul`. 

## BASE-LIBRARY REF Zero
Type u → Type u

Docstring: A type with a zero element. 

## BASE-LIBRARY REF Zero.zero
{α : Type u} → [self : Zero α] → α

Body:
fun α [self : Zero α] => self.1

Docstring: The zero element of the type. 

## BASE-LIBRARY REF MulZeroClass
Type u → Type u

Docstring: Typeclass for expressing that a type `M₀` with multiplication and a zero satisfies
`0 * a = 0` and `a * 0 = 0` for all `a : M₀`. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.zero_mul
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a : α), 0 * a = 0

Docstring: Zero is a left absorbing element for multiplication 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.mul_zero
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a : α), a * 0 = 0

Docstring: Zero is a right absorbing element for multiplication 

## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF EquivLike
Sort u_1 → outParam (Sort u_2) → outParam (Sort u_3) → Sort (max (max (max 1 u_1) u_2) u_3)

Docstring: The class `EquivLike E α β` expresses that terms of type `E` have an
injective coercion to bijections between `α` and `β`.

Note that this does not directly extend `FunLike`, nor take `FunLike` as a parameter,
so we can state `coe_injective'` in a nicer way.

This typeclass is used in the definition of the isomorphism (or equivalence) typeclasses,
such as `ZeroEquivClass`, `MulEquivClass`, `MonoidEquivClass`, ....


## BASE-LIBRARY REF EquivLike.coe
{E : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (Sort u_3)} → [self : EquivLike E α β] → E → α → β

Body:
fun E {α} {β} [self : EquivLike E α β] => self.1

Docstring: The coercion to a function in the forward direction. 

## BASE-LIBRARY REF EquivLike.toFunLike._proof_1
∀ {E : Sort u_3} {α : Sort u_1} {β : Sort u_2} [inst : EquivLike E α β] (e g : E),
  EquivLike.coe e = EquivLike.coe g → e = g

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

Body:
fun {α} {β} => { coe := Equiv.toFun, inv := Equiv.invFun, left_inv := ⋯, right_inv := ⋯, coe_injective' := ⋯ }

## BASE-LIBRARY REF Equiv.invFun
{α : Sort u_1} → {β : Sort u_2} → α ≃ β → β → α

Body:
fun α β self => self.2

Docstring: The backward map of an equivalence.

Do NOT use `e.invFun` directly. Use the coercion of `e.symm` instead. 

## BASE-LIBRARY REF Equiv.left_inv
∀ {α : Sort u_1} {β : Sort u_2} (self : α ≃ β), Function.LeftInverse self.invFun self.toFun

## BASE-LIBRARY REF Equiv.right_inv
∀ {α : Sort u_1} {β : Sort u_2} (self : α ≃ β), Function.RightInverse self.invFun self.toFun

## BASE-LIBRARY REF Equiv.instEquivLike._proof_1
∀ {α : Sort u_1} {β : Sort u_2} (e₁ e₂ : α ≃ β), e₁.toFun = e₂.toFun → e₁.invFun = e₂.invFun → e₁ = e₂

## BASE-LIBRARY REF Matrix.of
{m : Type u_2} → {n : Type u_3} → {α : Type v} → (m → n → α) ≃ Matrix m n α

Body:
fun {m} {n} {α} => Equiv.refl (m → n → α)

Docstring: Cast a function into a matrix.

The two sides of the equivalence are definitionally equal types. We want to use an explicit cast
to distinguish the types because `Matrix` has different instances to pi types (such as `Pi.mul`,
which performs elementwise multiplication, vs `Matrix.mul`).

If you are defining a matrix, in terms of its entries, use `of (fun i j ↦ _)`. The
purpose of this approach is to ensure that terms of the form `(fun i j ↦ _) * (fun i j ↦ _)` do not
appear, as the type of `*` can be misleading.


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


## BASE-LIBRARY REF Matrix.submatrix
{l : Type u_1} →
  {m : Type u_2} → {n : Type u_3} → {o : Type u_4} → {α : Type v} → Matrix m n α → (l → m) → (o → n) → Matrix l o α

Body:
fun {l} {m} {n} {o} {α} A r c => Matrix.of fun i j => A (r i) (c j)

Docstring: Given maps `(r : l → m)` and `(c : o → n)` reindexing the rows and columns of
a matrix `M : Matrix m n α`, the matrix `M.submatrix r c : Matrix l o α` is defined
by `(M.submatrix r c) i j = M (r i) (c j)` for `(i,j) : l × o`.
Note that the total number of row and columns does not have to be preserved. 

## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Body:
fun α => α ≃ α

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF Equiv.swap
{α : Sort u_1} → [DecidableEq α] → α → α → Equiv.Perm α

Body:
fun {α} [DecidableEq α] a b =>
  { toFun := Equiv.swapCore a b, invFun := Equiv.swapCore a b, left_inv := ⋯, right_inv := ⋯ }

Docstring: `swap a b` is the permutation that swaps `a` and `b` and
leaves other values as is. 

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Body:
fun α [self : Neg α] => self.1

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF NegZeroClass
Type u_2 → Type u_2

Docstring: Typeclass for expressing that `-0 = 0`. 

## BASE-LIBRARY REF SubNegZeroMonoid
Type u_2 → Type u_2

Docstring: A `SubNegMonoid` where `-0 = 0`. 

## BASE-LIBRARY REF SubNegZeroMonoid.neg_zero
∀ {G : Type u_2} [self : SubNegZeroMonoid G], -0 = 0

## BASE-LIBRARY REF SubtractionMonoid
Type u → Type u

Docstring: A `SubtractionMonoid` is a `SubNegMonoid` with involutive negation and such that
`-(a + b) = -b + -a` and `a + b = 0 → -a = b`. 

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


## BASE-LIBRARY REF SubtractionMonoid.toSubNegZeroMonoid._proof_1
∀ {α : Type u_1} [inst : SubtractionMonoid α], -0 = 0

## BASE-LIBRARY REF SubtractionCommMonoid
Type u → Type u

Docstring: Commutative `SubtractionMonoid`. 

## BASE-LIBRARY REF AddCommGroup
Type u → Type u

Docstring: An additive commutative group is an additive group with commutative `(+)`. 

## BASE-LIBRARY REF SubtractionMonoid.neg_neg
∀ {G : Type u} [self : SubtractionMonoid G] (x : G), - -x = x

## BASE-LIBRARY REF SubtractionMonoid.neg_add_rev
∀ {G : Type u} [self : SubtractionMonoid G] (a b : G), -(a + b) = -b + -a

## BASE-LIBRARY REF SubtractionMonoid.neg_eq_of_add
∀ {G : Type u} [self : SubtractionMonoid G] (a b : G), a + b = 0 → -a = b

Docstring: Despite the asymmetry of `neg_eq_of_add`, the symmetric version is true thanks to the
involutivity of negation. 

## BASE-LIBRARY REF LieRing
Type v → Type v

Docstring: A Lie ring is an additive group with compatible product, known as the bracket, satisfying the
Jacobi identity. 

## BASE-LIBRARY REF LieRing.ofAssociativeRing
{A : Type v} → [Ring A] → LieRing A

Body:
fun {A} [inst : Ring A] =>
  { toAddCommGroup := inst.toAddCommGroup, toBracket := Ring.instBracket, add_lie := ⋯, lie_add := ⋯, lie_self := ⋯,
    leibniz_lie := ⋯ }

Docstring: An associative ring gives rise to a Lie ring by taking the bracket to be the ring commutator. 

## INFORMAL STATEMENT
Column operation properties

Theorem~ \ref{thm.det.rowop} also holds if we replace “row” by “column” throughout it.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.det.k
conv.det.K

For the rest of this section, we fix a commutative ring $K$. In most examples, $K$ will be $\mathbb {Z}$ or $\mathbb {Q}$ or a polynomial ring.

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

## INFORMAL CONTEXT stmt-algebraic-combinatorics-thm.det.rowop
Row operation properties

Let $n \in \mathbb {N}$. Let $A \in K^{n \times n}$ be an $n \times n$-matrix. Then: 

\textbf{(a)} If we swap two rows of $A$, then $\det A$ gets multiplied by $-1$. 

\textbf{(b)} If $A$ has a zero row (i.e., a row that consists entirely of zeroes), then $\det A = 0$. 

\textbf{(c)} If $A$ has two equal rows, then $\det A = 0$. 

\textbf{(d)} Let $\lambda \in K$. If we multiply a row of $A$ by $\lambda $ (that is, we multiply all entries of this one row by $\lambda $, while leaving all other entries of $A$ unchanged), then $\det A$ gets multiplied by $\lambda $. 

\textbf{(e)} If we add a row of $A$ to another row of $A$ (that is, we add each entry of the former row to the corresponding entry of the latter), then $\det A$ stays unchanged. 

\textbf{(f)} Let $\lambda \in K$. If we add $\lambda $ times a row of $A$ to another row of $A$ (that is, we add $\lambda $ times each entry of the former row to the corresponding entry of the latter), then $\det A$ stays unchanged. 

\textbf{(g)} Let $B, C \in K^{n \times n}$ be two further $n \times n$-matrices. Let $k \in [n]$. Assume that 

\[  (\text{the } k\text{-th row of } C) = (\text{the } k\text{-th row of } A) + (\text{the } k\text{-th row of } B),  \]

 whereas each $i \neq k$ satisfies 

\[  (\text{the } i\text{-th row of } C) = (\text{the } i\text{-th row of } A) = (\text{the } i\text{-th row of } B).  \]

 Then, 

\[  \det C = \det A + \det B.  \]

## VERDICT
{
  "verdict": "faithful",
  "discrepancies": [],
  "justification": "The seven declarations exactly cover the column versions of clauses (a)\u2013(g) in the cited row-operation theorem. They use square matrices `Matrix (Fin n) (Fin n) K` over `[CommRing K]` and the Leibniz determinant `Matrix.det`, matching the blueprint\u2019s setting up to the routine zero-based `Fin n` encoding of `[n]`. In particular: `det_swap_cols` reindexes columns by `Equiv.swap i j` and concludes `=-A.det`; `det_zero_col` and `det_eq_cols` give determinant zero for a zero column and two distinct equal columns; `det_scale_col` replaces column `j` by `c * A i j` and concludes `c * A.det`; `det_add_col` and `det_add_smul_col` replace one column by itself plus another column or a scalar multiple thereof and preserve the determinant; and `det_col_add` assumes `C i k = A i k + B i k` together with `C i j = A i j \u2227 A i j = B i j` for every `j \u2260 k`, then concludes `C.det = A.det + B.det`. Quantifying over `K` and `n` rather than fixing them is more general and still certifies the informal claim."
}