## TARGET AlgebraicCombinatorics.Det.det_swap_rows (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {n : ℕ} (A : Matrix (Fin n) (Fin n) K) (i j : Fin n),
  i ≠ j → (Matrix.of (A ∘ ⇑(Equiv.swap i j))).det = -A.det

Docstring: (a) Swapping two rows multiplies determinant by -1.
Label: thm.det.rowop (a) 

## TARGET AlgebraicCombinatorics.Det.det_add_row (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {n : ℕ} (A : Matrix (Fin n) (Fin n) K) (i j : Fin n),
  i ≠ j → (A.updateRow i (A i + A j)).det = A.det

Docstring: (e) Adding one row to another preserves determinant (special case of (f)).
Label: thm.det.rowop (e) 

## TARGET AlgebraicCombinatorics.Det.det_eq_rows (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {n : ℕ} (A : Matrix (Fin n) (Fin n) K) (i j : Fin n), i ≠ j → A i = A j → A.det = 0

Docstring: (c) A matrix with two equal rows has determinant 0.
Label: thm.det.rowop (c) 

## TARGET AlgebraicCombinatorics.Det.det_zero_row (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {n : ℕ} (A : Matrix (Fin n) (Fin n) K) (i : Fin n),
  (∀ (j : Fin n), A i j = 0) → A.det = 0

Docstring: (b) A matrix with a zero row has determinant 0.
Label: thm.det.rowop (b) 

## TARGET AlgebraicCombinatorics.Det.det_add_smul_row (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {n : ℕ} (A : Matrix (Fin n) (Fin n) K) (i j : Fin n),
  i ≠ j → ∀ (c : K), (A.updateRow i (A i + c • A j)).det = A.det

Docstring: (f) Adding λ times one row to another preserves determinant.
Label: thm.det.rowop (f) 

## TARGET AlgebraicCombinatorics.Det.det_row_add (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {n : ℕ} (A B C : Matrix (Fin n) (Fin n) K) (k : Fin n),
  C k = A k + B k → (∀ (i : Fin n), i ≠ k → C i = A i ∧ A i = B i) → C.det = A.det + B.det

Docstring: (g) Multilinearity: determinant is additive in row k.
Label: thm.det.rowop (g) 

## TARGET AlgebraicCombinatorics.Det.det_scale_row (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {n : ℕ} (A : Matrix (Fin n) (Fin n) K) (i : Fin n) (c : K),
  (A.updateRow i (c • A i)).det = c * A.det

Docstring: (d) Scaling a row by λ scales the determinant by λ.
Label: thm.det.rowop (d) 

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


## BASE-LIBRARY REF Function.comp
{α : Sort u} → {β : Sort v} → {δ : Sort w} → (β → δ) → (α → β) → α → δ

Body:
fun {α} {β} {δ} f g x => f (g x)

Docstring: Function composition, usually written with the infix operator `∘`. A new function is created from
two existing functions, where one function's output is used as input to the other.

Examples:
 * `Function.comp List.reverse (List.drop 2) [3, 2, 4, 1] = [1, 4]`
 * `(List.reverse ∘ List.drop 2) [3, 2, 4, 1] = [1, 4]`


Conventions for notations in identifiers:

 * The recommended spelling of `∘` in identifiers is `comp`.

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

## BASE-LIBRARY REF AddCommGroup.add_comm
∀ {G : Type u} [self : AddCommGroup G] (a b : G), a + b = b + a

Docstring: Addition is commutative in a commutative additive magma. 

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

## BASE-LIBRARY REF Matrix.updateRow
{m : Type u_2} → {n : Type u_3} → {α : Type v} → [DecidableEq m] → Matrix m n α → m → (n → α) → Matrix m n α

Body:
fun {m} {n} {α} [DecidableEq m] M i b => Matrix.of (Function.update M i b)

Docstring: Update, i.e. replace the `i`th row of matrix `A` with the values in `b`. 

## BASE-LIBRARY REF Add
Type u → Type u

Docstring: The homogeneous version of `HAdd`: `a + b : α` where `a b : α`. 

## BASE-LIBRARY REF Add.add
{α : Type u} → [self : Add α] → α → α → α

Body:
fun α [self : Add α] => self.1

Docstring: `a + b` computes the sum of `a` and `b`. See `HAdd`. 

## BASE-LIBRARY REF Pi.instAdd
{ι : Type u_1} → {M : ι → Type u_5} → [(i : ι) → Add (M i)] → Add ((i : ι) → M i)

Body:
fun {ι} {M} [(i : ι) → Add (M i)] => { add := fun f g i => f i + g i }

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

## BASE-LIBRARY REF NonUnitalNonAssocRing.left_distrib
∀ {α : Type u} [self : NonUnitalNonAssocRing α] (a b c : α), a * (b + c) = a * b + a * c

Docstring: Multiplication is left distributive over addition 

## BASE-LIBRARY REF NonUnitalNonAssocRing.right_distrib
∀ {α : Type u} [self : NonUnitalNonAssocRing α] (a b c : α), (a + b) * c = a * c + b * c

Docstring: Multiplication is right distributive over addition 

## BASE-LIBRARY REF NonUnitalNonAssocRing.zero_mul
∀ {α : Type u} [self : NonUnitalNonAssocRing α] (a : α), 0 * a = 0

Docstring: Zero is a left absorbing element for multiplication 

## BASE-LIBRARY REF NonUnitalNonAssocRing.mul_zero
∀ {α : Type u} [self : NonUnitalNonAssocRing α] (a : α), a * 0 = 0

Docstring: Zero is a right absorbing element for multiplication 

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

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing._proof_1
∀ {α : Type u_1} [s : CommRing α] (a b : α), a - b = a + -b

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

## BASE-LIBRARY REF SMul
Type u → Type v → Type (max u v)

Docstring: Typeclass for types with a scalar multiplication operation, denoted `•` (`\bu`) 

## BASE-LIBRARY REF SMul.smul
{M : Type u} → {α : Type v} → [self : SMul M α] → M → α → α

Body:
fun M α [self : SMul M α] => self.1

Docstring: `m • a : α` denotes the product of `m : M` and `a : α`. The meaning of this notation is type-dependent,
but it is intended to be used for left actions. 

## BASE-LIBRARY REF Function.hasSMul
{ι : Type u_1} → {M : Type u_2} → {α : Type u_7} → [SMul M α] → SMul M (ι → α)

Body:
fun {ι} {M} {α} [SMul M α] => Pi.instSMul

Docstring: Non-dependent version of `Pi.smul`. Lean gets confused by the dependent instance if this
is not present. 

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF Semiring
Type u → Type u

Docstring: A `Semiring` is a type with addition, multiplication, a `0` and a `1` where addition is
commutative and associative, multiplication is associative and left and right distributive over
addition, and `0` and `1` are additive and multiplicative identities. 

## BASE-LIBRARY REF Algebra
(R : Type u) → (A : Type v) → [CommSemiring R] → [Semiring A] → Type (max u v)

Docstring: An associative unital `R`-algebra is a semiring `A` equipped with a map into its center `R → A`.

See the implementation notes in this file for discussion of the details of this definition.


## BASE-LIBRARY REF CommRing.mul_comm
∀ {α : Type u} [self : CommRing α] (a b : α), a * b = b * a

Docstring: Multiplication is commutative in a commutative multiplicative magma. 

## BASE-LIBRARY REF Algebra.id
(R : Type u) → [inst : CommSemiring R] → Algebra R R

Docstring: The identity map inducing an `Algebra` structure. 

## BASE-LIBRARY REF Mul
Type u → Type u

Docstring: The homogeneous version of `HMul`: `a * b : α` where `a b : α`. 

## BASE-LIBRARY REF Mul.mul
{α : Type u} → [self : Mul α] → α → α → α

Body:
fun α [self : Mul α] => self.1

Docstring: `a * b` computes the product of `a` and `b`. See `HMul`. 

## INFORMAL STATEMENT
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

## VERDICT
{
  "verdict": "significant_divergence",
  "discrepancies": [
    {
      "root": "[inst : CommRing K]",
      "severity": "significant",
      "bridge": "The blueprint would be recovered only by adding that K is a commutative ring, or by proving all seven properties for every algebraic setting in which its displayed Leibniz formula makes sense. The package supplies no such assumption on K. Moreover, the unrestricted extension is not generally available: over a noncommutative ring, for example, scaling a noninitial row need not multiply the ordered Leibniz determinant on the left by \u03bb. Thus commutativity cannot be discharged as a routine encoding condition."
    }
  ],
  "justification": "Every elaborated target restricts the coefficient type by `\u2200 {K : Type u_1} [inst : CommRing K] ...`. In contrast, the blueprint only says `Let A \u2208 K^{n \u00d7 n}` and, in (d) and (f), `Let \u03bb \u2208 K`, without specifying that K is a commutative ring. Its determinant definition likewise gives the Leibniz sum as an element `of K` but imposes no algebraic hypothesis on K. The row indexing by `Fin n`, `updateRow` formulations, distinctness assumptions for \u201ctwo/another\u201d rows, and the hypotheses in (g) otherwise faithfully encode the seven claims."
}