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

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Body:
fun {α} s => s.val.card

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

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

## BASE-LIBRARY REF Matrix.submatrix
{l : Type u_1} →
  {m : Type u_2} → {n : Type u_3} → {o : Type u_4} → {α : Type v} → Matrix m n α → (l → m) → (o → n) → Matrix l o α

Body:
fun {l} {m} {n} {o} {α} A r c => Matrix.of fun i j => A (r i) (c j)

Docstring: Given maps `(r : l → m)` and `(c : o → n)` reindexing the rows and columns of
a matrix `M : Matrix m n α`, the matrix `M.submatrix r c : Matrix l o α` is defined
by `(M.submatrix r c) i j = M (r i) (c j)` for `(i,j) : l × o`.
Note that the total number of row and columns does not have to be preserved. 

## BASE-LIBRARY REF Matrix.diagonal
{n : Type u_3} → {α : Type v} → [DecidableEq n] → [Zero α] → (n → α) → Matrix n n α

Body:
fun {n} {α} [DecidableEq n] [Zero α] d => Matrix.of fun i j => if i = j then d i else 0

Docstring: `diagonal d` is the square matrix such that `(diagonal d) i i = d i` and `(diagonal d) i j = 0`
if `i ≠ j`.

Note that bundled versions exist as:
* `Matrix.diagonalAddMonoidHom`
* `Matrix.diagonalLinearMap`
* `Matrix.diagonalRingHom`
* `Matrix.diagonalAlgHom`


## BASE-LIBRARY REF MulZeroClass
Type u → Type u

Docstring: Typeclass for expressing that a type `M₀` with multiplication and a zero satisfies
`0 * a = 0` and `a * 0 = 0` for all `a : M₀`. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring
Type u → Type u

Docstring: A not-necessarily-unital, not-necessarily-associative semiring. See `CommutatorRing` and the
documentation thereof in case you need a `NonUnitalNonAssocSemiring` instance on a Lie ring
or a Lie algebra. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.zero_mul
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a : α), 0 * a = 0

Docstring: Zero is a left absorbing element for multiplication 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.mul_zero
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a : α), a * 0 = 0

Docstring: Zero is a right absorbing element for multiplication 

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

## BASE-LIBRARY REF OrderEmbedding
(α : Type u_6) → (β : Type u_7) → [LE α] → [LE β] → Type (max u_6 u_7)

Body:
fun α β [LE α] [LE β] => (fun x1 x2 => x1 ≤ x2) ↪r fun x1 x2 => x1 ≤ x2

Docstring: An order embedding is an embedding `f : α ↪ β` such that `a ≤ b ↔ (f a) ≤ (f b)`.
This definition is an abbreviation of `RelEmbedding (≤) (≤)`. 

## BASE-LIBRARY REF Preorder
Type u_2 → Type u_2

Docstring: A preorder is a reflexive, transitive relation `≤`.
In a preorder, `a < b` means `a ≤ b ∧ ¬b ≤ a`, and `<` is defined this way by default.
You can override this definition to set a better def-eq.


## BASE-LIBRARY REF PartialOrder
Type u_2 → Type u_2

Docstring: A partial order is a reflexive, transitive, antisymmetric relation `≤`. 

## BASE-LIBRARY REF SemilatticeInf
Type u → Type u

Docstring: A `SemilatticeInf` is a meet-semilattice, that is, a partial order
with a meet (a.k.a. glb / greatest lower bound, inf / infimum) operation
`⊓` which is the greatest element smaller than both factors. 

## BASE-LIBRARY REF Lattice
Type u → Type u

Docstring: A lattice is a join-semilattice which is also a meet-semilattice. 

## BASE-LIBRARY REF Lattice.inf
{α : Type u} → [self : Lattice α] → α → α → α

Body:
fun α [self : Lattice α] => self.2

Docstring: The binary infimum, used to derive `Min α` 

## BASE-LIBRARY REF Lattice.inf_le_left
∀ {α : Type u} [self : Lattice α] (a b : α), Lattice.inf a b ≤ a

Docstring: The infimum is a lower bound on the first argument 

## BASE-LIBRARY REF Lattice.inf_le_right
∀ {α : Type u} [self : Lattice α] (a b : α), Lattice.inf a b ≤ b

Docstring: The infimum is a lower bound on the second argument 

## BASE-LIBRARY REF Lattice.le_inf
∀ {α : Type u} [self : Lattice α] (a b c : α), a ≤ b → a ≤ c → a ≤ Lattice.inf b c

Docstring: The infimum is the *greatest* lower bound 

## BASE-LIBRARY REF DistribLattice
Type u_1 → Type u_1

Docstring: A distributive lattice is a lattice that satisfies any of four
equivalent distributive properties (of `sup` over `inf` or `inf` over `sup`,
on the left or right).

The definition here chooses `le_sup_inf`: `(x ⊔ y) ⊓ (x ⊔ z) ≤ x ⊔ (y ⊓ z)`. To prove distributivity
from the dual law, use `DistribLattice.of_inf_sup_le`.

A classic example of a distributive lattice
is the lattice of subsets of a set, and in fact this example is
generic in the sense that every distributive lattice is realizable
as a sublattice of a powerset lattice. 

## BASE-LIBRARY REF LinearOrder
Type u_2 → Type u_2

Docstring: A linear order is reflexive, transitive, antisymmetric and total relation `≤`.
We assume that every linear ordered type has decidable `(≤)`, `(<)`, and `(=)`. 

## BASE-LIBRARY REF instDistribLatticeOfLinearOrder._proof_4
∀ {α : Type u_1} [inst : LinearOrder α] (x b c : α), min (max x b) (max x c) ≤ max x (min b c)

## BASE-LIBRARY REF Fin.instLinearOrder
{n : ℕ} → LinearOrder (Fin n)

Body:
fun {n} => Function.Injective.linearOrder Fin.val ⋯ ⋯ ⋯ ⋯ ⋯ ⋯

## BASE-LIBRARY REF Function.Injective.linearOrder
{α : Type u_2} →
  {β : Type u_3} →
    [inst : LinearOrder β] →
      [inst_1 : LE α] →
        [inst_2 : LT α] →
          [inst_3 : Max α] →
            [inst_4 : Min α] →
              [inst_5 : Ord α] →
                [DecidableEq α] →
                  [DecidableLE α] →
                    [DecidableLT α] →
                      (f : α → β) →
                        Function.Injective f →
                          (∀ {x y : α}, f x ≤ f y ↔ x ≤ y) →
                            (∀ {x y : α}, f x < f y ↔ x < y) →
                              (∀ (x y : α), f (x ⊓ y) = min (f x) (f y)) →
                                (∀ (x y : α), f (x ⊔ y) = max (f x) (f y)) →
                                  (∀ (x y : α), compare (f x) (f y) = compare x y) → LinearOrder α

Docstring: Pull back a `LinearOrder` instance along an injective function.

See note [reducible non-instances]. 

## BASE-LIBRARY REF Nat.instLinearOrder
LinearOrder ℕ

Body:
{ le := Nat.le, lt := Nat.lt, le_refl := Nat.le_refl, le_trans := @Nat.le_trans,
  lt_iff_le_not_ge := @Nat.lt_iff_le_not_le, le_antisymm := @Nat.le_antisymm, toMin := instMinNat, toMax := Nat.instMax,
  toOrd := instOrdNat, le_total := Nat.le_total, toDecidableLE := inferInstance, toDecidableEq := inferInstance,
  toDecidableLT := inferInstance, min_def := Nat.instLinearOrder._proof_1, max_def := Nat.instLinearOrder._proof_2,
  compare_eq_compareOfLessAndEq := Nat.instLinearOrder._proof_3 }

## BASE-LIBRARY REF Fin.instMax_mathlib
{n : ℕ} → Max (Fin n)

Body:
fun {n} => { max := fun x y => ⟨max ↑x ↑y, ⋯⟩ }

## BASE-LIBRARY REF Fin.instMin_mathlib
{n : ℕ} → Min (Fin n)

Body:
fun {n} => { min := fun x y => ⟨min ↑x ↑y, ⋯⟩ }

## BASE-LIBRARY REF Fin.decLe
{n : ℕ} → (a b : Fin n) → Decidable (a ≤ b)

Body:
fun {n} a b => (↑a).decLe ↑b

## BASE-LIBRARY REF Fin.decLt
{n : ℕ} → (a b : Fin n) → Decidable (a < b)

Body:
fun {n} a b => (↑a).decLt ↑b

## BASE-LIBRARY REF Fin.val_injective
∀ {n : ℕ}, Function.Injective Fin.val

## BASE-LIBRARY REF Fin.le_iff_val_le_val
∀ {n : ℕ} {a b : Fin n}, a ≤ b ↔ ↑a ≤ ↑b

## BASE-LIBRARY REF Fin.lt_def
∀ {n : ℕ} {a b : Fin n}, a < b ↔ ↑a < ↑b

## BASE-LIBRARY REF Fin.coe_min
∀ {n : ℕ} (a b : Fin n), ↑(min a b) = min ↑a ↑b

## BASE-LIBRARY REF LE
Type u → Type u

Docstring: `LE α` is the typeclass which supports the notation `x ≤ y` where `x y : α`.

## BASE-LIBRARY REF RelEmbedding.instFunLike
{α : Type u_1} → {β : Type u_2} → {r : α → α → Prop} → {s : β → β → Prop} → FunLike (r ↪r s) α β

Body:
fun {α} {β} {r} {s} => { coe := fun x => x.toFun, coe_injective' := ⋯ }

## BASE-LIBRARY REF Finset.orderEmbOfFin
{α : Type u_1} → [inst : LinearOrder α] → (s : Finset α) → {k : ℕ} → s.card = k → Fin k ↪o α

Body:
fun {α} [LinearOrder α] s {k} h =>
  RelEmbedding.trans (s.orderIsoOfFin h).toOrderEmbedding (OrderEmbedding.subtype fun x => x ∈ s)

Docstring: Given a finset `s` of cardinality `k` in a linear order `α`, the map `orderEmbOfFin s h` is
the increasing bijection between `Fin k` and `s` as an order embedding into `α`. Here, `h` is a
proof that the cardinality of `s` is `k`. We use this instead of an embedding `Fin s.card ↪o α` to
avoid casting issues in further uses of this function. 

## BASE-LIBRARY REF rfl
∀ {α : Sort u} {a : α}, a = a

Body:
fun {α} {a} => Eq.refl a

Docstring: `rfl : a = a` is the unique constructor of the equality type. This is the
same as `Eq.refl` except that it takes `a` implicitly instead of explicitly.

This is a more powerful theorem than it may appear at first, because although
the statement of the theorem is `a = a`, Lean will allow anything that is
definitionally equal to that type. So, for instance, `2 + 2 = 4` is proven in
Lean by `rfl`, because both sides are the same up to definitional equality.


## BASE-LIBRARY REF Eq.rec
{α : Sort u_1} →
  {a : α} → {motive : (a_1 : α) → a = a_1 → Sort u} → motive a ⋯ → {a_1 : α} → (t : a = a_1) → motive a_1 t

## BASE-LIBRARY REF Zero
Type u → Type u

Docstring: A type with a zero element. 

## BASE-LIBRARY REF Zero.zero
{α : Type u} → [self : Zero α] → α

Body:
fun α [self : Zero α] => self.1

Docstring: The zero element of the type. 

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Body:
fun {ι} {M} [CommMonoid M] s f => (Multiset.map f s.val).prod

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF NonUnitalSemiring.mul_assoc
∀ {α : Type u} [self : NonUnitalSemiring α] (a b c : α), a * b * c = a * (b * c)

Docstring: Multiplication is associative 

## BASE-LIBRARY REF Semiring.one_mul
∀ {α : Type u} [self : Semiring α] (a : α), 1 * a = a

Docstring: One is a left neutral element for multiplication 

## BASE-LIBRARY REF Semiring.mul_one
∀ {α : Type u} [self : Semiring α] (a : α), a * 1 = a

Docstring: One is a right neutral element for multiplication 

## BASE-LIBRARY REF CommRing.mul_comm
∀ {α : Type u} [self : CommRing α] (a b : α), a * b = b * a

Docstring: Multiplication is commutative in a commutative multiplicative magma. 

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
  "verdict": "faithful",
  "discrepancies": [],
  "justification": "The two formal theorems exactly cover both blueprint clauses. For (a), the formal conclusion `((Matrix.diagonal d).submatrix \u21d1(P.orderEmbOfFin \u22ef) \u21d1(P.orderEmbOfFin \u22ef)).det = \u220f i \u2208 P, d i` matches `det (sub_P^P D) = \u220f_{i\u2208P} d_i`. For (b), the binders `P Q : Finset (Fin n)`, `hcard : P.card = Q.card`, and hypothesis `P \u2260 Q` match \u201ctwo distinct subsets of [n] satisfying |P|=|Q|,\u201d while the conclusion gives determinant zero. `Fin n` versus `[n]`, the zero-based encoding of `d\u2081,\u2026,d\u2099` as `d : Fin n \u2192 R`, and the increasing enumerations supplied by `Finset.orderEmbOfFin` are notational re-encodings. The `CommRing R` assumption is the algebraic structure needed by the formal determinant and includes the conventional field-valued case suggested by `K`."
}