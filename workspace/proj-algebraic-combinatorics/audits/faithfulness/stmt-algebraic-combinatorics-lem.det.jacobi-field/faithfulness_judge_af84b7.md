## TARGET AlgebraicCombinatorics.Determinants.jacobi_complementary_minor_field (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_2} [inst : Field K] {m : ℕ} (A : Matrix (Fin m) (Fin m) K),
  A.det ≠ 0 →
    ∀ (P Q : Finset (Fin m)) (hPQ : P.card = Q.card),
      P.card ≥ 1 →
        (A.adjugate.submatrix ⇑(AlgebraicCombinatorics.Determinants.finsetOrderEmb P) fun i =>
              (AlgebraicCombinatorics.Determinants.finsetOrderEmb Q) ((finCongr hPQ) i)).det =
          (-1) ^ (P.sum Fin.val + Q.sum Fin.val) * A.det ^ (Q.card - 1) *
            (A.submatrix ⇑(AlgebraicCombinatorics.Determinants.finsetOrderEmb Qᶜ) fun i =>
                (AlgebraicCombinatorics.Determinants.finsetOrderEmb Pᶜ) ((finCongr ⋯) i)).det

Docstring: Corollary: For invertible A with |P| = |Q| = k, the determinant of the adjugate submatrix
can be computed from the complementary minor of A.

det(sub_P^Q(adj A)) = (-1)^(sum P + sum Q) * det(A)^(k-1) * det(sub_{Qᶜ}^{Pᶜ}(A))

This follows from:
- adj(A) = det(A) * A⁻¹ for invertible A
- det(sub_P^Q(adj A)) = det(A)^k * det(sub_P^Q(A⁻¹))
- complementary_minor_inverse: det(A) * det(sub_P^Q(A⁻¹)) = (-1)^(...) * det(sub_{Qᶜ}^{Pᶜ}(A)) 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Determinants.finsetOrderEmb (def)
{m : ℕ} → (P : Finset (Fin m)) → Fin P.card ↪ Fin m

Body:
fun {m} P => (P.orderIsoOfFin ⋯).toEmbedding.trans (Function.Embedding.subtype fun x => x ∈ P)

Docstring: Helper: convert orderIsoOfFin to an embedding from Fin |P| to Fin m.
This gives an order-preserving embedding that picks out the elements of P. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Determinants.submatrixDet (def)
{R : Type u_1} → [CommRing R] → {m : ℕ} → Matrix (Fin m) (Fin m) R → Finset (Fin m) → Finset (Fin m) → R

Body:
fun {R} [CommRing R] {m} A P Q =>
  if h : P.card = Q.card then (AlgebraicCombinatorics.Determinants.submatrixOfFinsets' A P Q ⋯ ⋯).det else 0

Docstring: The determinant of a submatrix corresponding to row set P and column set Q.
Returns 0 if |P| ≠ |Q|. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Determinants.submatrixOfFinsets' (def)
{R : Type u_1} →
  {m k : ℕ} → Matrix (Fin m) (Fin m) R → (P Q : Finset (Fin m)) → P.card = k → Q.card = k → Matrix (Fin k) (Fin k) R

Body:
fun {R} {m k} A P Q hP hQ =>
  A.submatrix ⇑(AlgebraicCombinatorics.Determinants.finsetToFin P hP)
    ⇑(AlgebraicCombinatorics.Determinants.finsetToFin Q hQ)

Docstring: The submatrix of A with rows from P and columns from Q (when |P| = |Q|).
This is the minor sub_P^Q(A) in the source notation. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Determinants.finsetToFin (def)
{m k : ℕ} → (S : Finset (Fin m)) → S.card = k → Fin k ↪ Fin m

Body:
fun {m k} S hk => (S.orderIsoOfFin hk).toEmbedding.trans (Function.Embedding.subtype fun x => x ∈ S)

Docstring: Helper: Given a finset of indices, produce an order-preserving embedding into Fin m.
This is used to extract submatrices corresponding to index subsets. 

## BASE-LIBRARY REF Field
Type u → Type u

Docstring: A `Field` is a `CommRing` with multiplicative inverses for nonzero elements.

An instance of `Field K` includes maps `ratCast : ℚ → K` and `qsmul : ℚ → K → K`.
Those two fields are needed to implement the `DivisionRing K → Algebra ℚ K` instance since we need
to control the specific definitions for some special cases of `K` (in particular `K = ℚ` itself).
See also note [forgetful inheritance].

If the field has positive characteristic `p`, our division by zero convention forces
`ratCast (1 / p) = 1 / 0 = 0`. 

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

## BASE-LIBRARY REF EuclideanDomain.toCommRing
{R : Type u} → [self : EuclideanDomain R] → CommRing R

## BASE-LIBRARY REF Field.toEuclideanDomain
{K : Type u_1} → [Field K] → EuclideanDomain K

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

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

## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Matrix.submatrix
{l : Type u_1} →
  {m : Type u_2} → {n : Type u_3} → {o : Type u_4} → {α : Type v} → Matrix m n α → (l → m) → (o → n) → Matrix l o α

Docstring: Given maps `(r : l → m)` and `(c : o → n)` reindexing the rows and columns of
a matrix `M : Matrix m n α`, the matrix `M.submatrix r c : Matrix l o α` is defined
by `(M.submatrix r c) i j = M (r i) (c j)` for `(i,j) : l × o`.
Note that the total number of row and columns does not have to be preserved. 

## BASE-LIBRARY REF Matrix.adjugate
{n : Type v} → {α : Type w} → [DecidableEq n] → [Fintype n] → [CommRing α] → Matrix n n α → Matrix n n α

Docstring: The adjugate matrix is the transpose of the cofactor matrix.

Typically, the cofactor matrix is defined by taking minors,
i.e. the determinant of the matrix with a row and column removed.
However, the proof of `mul_adjugate` becomes a lot easier if we use the
matrix replacing a column with a basis vector, since it allows us to use
facts about the `cramer` map.


## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF Function.Embedding
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ↪ β` is a bundled injective function. 

## BASE-LIBRARY REF Function.instFunLikeEmbedding
{α : Sort u} → {β : Sort v} → FunLike (α ↪ β) α β

## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

## BASE-LIBRARY REF finCongr
{n m : ℕ} → n = m → Fin n ≃ Fin m

Docstring: The 'identity' equivalence between `Fin m` and `Fin n` when `m = n`. 

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

## BASE-LIBRARY REF HPow.hPow
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HPow α β γ] → α → β → γ

Docstring: `a ^ b` computes `a` to the power of `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `^` in identifiers is `pow`.

## BASE-LIBRARY REF instHPow
{α : Type u_1} → {β : Type u_2} → [Pow α β] → HPow α β α

## BASE-LIBRARY REF Monoid.toNatPow
{M : Type u_2} → [Monoid M] → Pow M ℕ

## BASE-LIBRARY REF MonoidWithZero.toMonoid
{M₀ : Type u} → [self : MonoidWithZero M₀] → Monoid M₀

## BASE-LIBRARY REF Semiring.toMonoidWithZero
{α : Type u} → [self : Semiring α] → MonoidWithZero α

## BASE-LIBRARY REF DivisionSemiring.toSemiring
{K : Type u_2} → [self : DivisionSemiring K] → Semiring K

## BASE-LIBRARY REF Semifield.toDivisionSemiring
{K : Type u_2} → [self : Semifield K] → DivisionSemiring K

## BASE-LIBRARY REF Field.toSemifield
{K : Type u_1} → [Field K] → Semifield K

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF NegZeroClass.toNeg
{G : Type u_2} → [self : NegZeroClass G] → Neg G

## BASE-LIBRARY REF SubNegZeroMonoid.toNegZeroClass
{G : Type u_2} → [self : SubNegZeroMonoid G] → NegZeroClass G

## BASE-LIBRARY REF SubtractionMonoid.toSubNegZeroMonoid
{α : Type u_1} → [SubtractionMonoid α] → SubNegZeroMonoid α

## BASE-LIBRARY REF SubtractionCommMonoid.toSubtractionMonoid
{G : Type u} → [self : SubtractionCommMonoid G] → SubtractionMonoid G

## BASE-LIBRARY REF AddCommGroup.toDivisionAddCommMonoid
{G : Type u_1} → [AddCommGroup G] → SubtractionCommMonoid G

## BASE-LIBRARY REF LieRing.toAddCommGroup
{L : Type v} → [self : LieRing L] → AddCommGroup L

## BASE-LIBRARY REF LieRing.ofAssociativeRing
{A : Type v} → [Ring A] → LieRing A

Docstring: An associative ring gives rise to a Lie ring by taking the bracket to be the ring commutator. 

## BASE-LIBRARY REF DivisionRing.toRing
{K : Type u_2} → [self : DivisionRing K] → Ring K

## BASE-LIBRARY REF Field.toDivisionRing
{K : Type u} → [self : Field K] → DivisionRing K

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF AddMonoidWithOne.toOne
{R : Type u_2} → [self : AddMonoidWithOne R] → One R

## BASE-LIBRARY REF AddGroupWithOne.toAddMonoidWithOne
{R : Type u} → [self : AddGroupWithOne R] → AddMonoidWithOne R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

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

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF instSubNat
Sub ℕ

## BASE-LIBRARY REF Compl.compl
{α : Type u_1} → [self : Compl α] → α → α

Docstring: Set / lattice complement 

Conventions for notations in identifiers:

 * The recommended spelling of `ᶜ` in identifiers is `compl`.

## BASE-LIBRARY REF BooleanAlgebra.toCompl
{α : Type u} → [self : BooleanAlgebra α] → Compl α

## BASE-LIBRARY REF Finset.booleanAlgebra
{α : Type u_1} → [Fintype α] → [DecidableEq α] → BooleanAlgebra (Finset α)

## BASE-LIBRARY REF of_eq_true
∀ {p : Prop}, p = True → p

## BASE-LIBRARY REF Eq.trans
∀ {α : Sort u} {a b c : α}, a = b → b = c → a = c

Docstring: Equality is transitive: if `a = b` and `b = c` then `a = c`.

Because this is in the `Eq` namespace, if you have variables or expressions
`h₁ : a = b` and `h₂ : b = c`, you can use `h₁.trans h₂ : a = c` as shorthand
for `Eq.trans h₁ h₂`.

For more information: [Equality](https://lean-lang.org/theorem_proving_in_lean4/quantifiers_and_equality.html#equality)


## BASE-LIBRARY REF True
Prop

Docstring: `True` is a proposition and has only an introduction rule, `True.intro : True`.
In other words, `True` is simply true, and has a canonical proof, `True.intro`
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


## BASE-LIBRARY REF congr
∀ {α : Sort u} {β : Sort v} {f₁ f₂ : α → β} {a₁ a₂ : α}, f₁ = f₂ → a₁ = a₂ → f₁ a₁ = f₂ a₂

Docstring: Congruence in both function and argument. If `f₁ = f₂` and `a₁ = a₂` then
`f₁ a₁ = f₂ a₂`. This only works for nondependent functions; the theorem
statement is more complex in the dependent case.

For more information: [Equality](https://lean-lang.org/theorem_proving_in_lean4/quantifiers_and_equality.html#equality)


## BASE-LIBRARY REF congrArg
∀ {α : Sort u} {β : Sort v} {a₁ a₂ : α} (f : α → β), a₁ = a₂ → f a₁ = f a₂

Docstring: Congruence in the function argument: if `a₁ = a₂` then `f a₁ = f a₂` for
any (nondependent) function `f`. This is more powerful than it might look at first, because
you can also use a lambda expression for `f` to prove that
`<something containing a₁> = <something containing a₂>`. This function is used
internally by tactics like `congr` and `simp` to apply equalities inside
subterms.

For more information: [Equality](https://lean-lang.org/theorem_proving_in_lean4/quantifiers_and_equality.html#equality)


## BASE-LIBRARY REF Fintype.card
(α : Type u_4) → [Fintype α] → ℕ

Docstring: `card α` is the number of elements in `α`, defined when `α` is a fintype. 

## BASE-LIBRARY REF Finset.card_compl
∀ {α : Type u_1} [inst : DecidableEq α] [inst_1 : Fintype α] (s : Finset α), sᶜ.card = Fintype.card α - s.card

## BASE-LIBRARY REF congrFun'
∀ {α : Sort u} {β : Sort v} {f g : α → β}, f = g → ∀ (a : α), f a = g a

Docstring: Similar to `congrFun` but `β` does not depend on `α`. 

## BASE-LIBRARY REF Fintype.card_fin
∀ (n : ℕ), Fintype.card (Fin n) = n

## BASE-LIBRARY REF eq_self
∀ {α : Sort u_1} (a : α), (a = a) = True

## BASE-LIBRARY REF Function.Embedding.trans
{α : Sort u_1} → {β : Sort u_2} → {γ : Sort u_3} → (α ↪ β) → (β ↪ γ) → α ↪ γ

Docstring: Composition of `f : α ↪ β` and `g : β ↪ γ`. 

## BASE-LIBRARY REF Subtype
{α : Sort u} → (α → Prop) → Sort (max 1 u)

Docstring: All the elements of a type that satisfy a predicate.

`Subtype p`, usually written `{ x : α // p x }` or `{ x // p x }`, contains all elements `x : α` for
which `p x` is true. Its constructor is a pair of the value and the proof that it satisfies the
predicate. In run-time code, `{ x : α // p x }` is represented identically to `α`.

There is a coercion from `{ x : α // p x }` to `α`, so elements of a subtype may be used where the
underlying type is expected.

Examples:
 * `{ n : Nat // n % 2 = 0 }` is the type of even numbers.
 * `{ xs : Array String // xs.size = 5 }` is the type of arrays with five `String`s.
 * Given `xs : List α`, `List { x : α // x ∈ xs }` is the type of lists in which all elements are
   contained in `xs`.


Conventions for notations in identifiers:

 * The recommended spelling of `{ x // p x }` in identifiers is `subtype`.

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF SetLike.instMembership
{A : Type u_1} → {B : Type u_2} → [i : SetLike A B] → Membership B A

## BASE-LIBRARY REF Finset.instSetLike
{α : Type u_1} → SetLike (Finset α) α

Docstring: Convert a finset to a set in the natural way. 

## BASE-LIBRARY REF Equiv.toEmbedding
{α : Sort u} → {β : Sort v} → α ≃ β → α ↪ β

Docstring: Convert an `α ≃ β` to `α ↪ β`.

This is also available as a coercion `Equiv.coeEmbedding`.
The explicit `Equiv.toEmbedding` version is preferred though, since the coercion can have issues
inferring the type of the resulting embedding. For example:

```lean
-- Works:
example (s : Finset (Fin 3)) (f : Equiv.Perm (Fin 3)) : s.map f.toEmbedding = s.map f := by simp
-- Error, `f` has type `Fin 3 ≃ Fin 3` but is expected to have type `Fin 3 ↪ ?m_1 : Type ?`
example (s : Finset (Fin 3)) (f : Equiv.Perm (Fin 3)) : s.map f = s.map f.toEmbedding := by simp
```


## BASE-LIBRARY REF RelIso.toEquiv
{α : Type u_5} → {β : Type u_6} → {r : α → α → Prop} → {s : β → β → Prop} → r ≃r s → α ≃ β

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLEFin
{n : ℕ} → LE (Fin n)

## BASE-LIBRARY REF Subtype.instLE
{α : Type u} → [LE α] → {P : α → Prop} → LE (Subtype P)

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

## BASE-LIBRARY REF Finset.orderIsoOfFin
{α : Type u_1} → [inst : LinearOrder α] → (s : Finset α) → {k : ℕ} → s.card = k → Fin k ≃o ↥s

Docstring: Given a finset `s` of cardinality `k` in a linear order `α`, the map `orderIsoOfFin s h`
is the increasing bijection between `Fin k` and `s` as an `OrderIso`. Here, `h` is a proof that
the cardinality of `s` is `k`. We use this instead of an iso `Fin s.card ≃o s` to avoid
casting issues in further uses of this function. 

## BASE-LIBRARY REF Function.Embedding.subtype
{α : Sort u_1} → (p : α → Prop) → Subtype p ↪ α

Docstring: Embedding of a `Subtype`. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF dite
{α : Sort u} → (c : Prop) → [h : Decidable c] → (c → α) → (¬c → α) → α

Docstring: "Dependent" if-then-else, normally written via the notation `if h : c then t(h) else e(h)`,
is sugar for `dite c (fun h => t(h)) (fun h => e(h))`, and it is the same as
`if c then t else e` except that `t` is allowed to depend on a proof `h : c`,
and `e` can depend on `h : ¬c`. (Both branches use the same name for the hypothesis,
even though it has different types in the two cases.)

We use this to be able to communicate the if-then-else condition to the branches.
For example, `Array.get arr i h` expects a proof `h : i < arr.size` in order to
avoid a bounds check, so you can write `if h : i < arr.size then arr.get i h else ...`
to avoid the bounds check inside the if branch. (Of course in this case we have only
lifted the check into an explicit `if`, but we could also use this proof multiple times
or derive `i < arr.size` from some other proposition that we are checking in the `if`.)


## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## INFORMAL STATEMENT
lem.det.jacobi-field

\leanhelper  Let $K$ be a field. Let $A \in K^{m \times m}$ with $\det A \neq 0$. Let $P, Q \subseteq [m]$ with $|P| = |Q| \geq 1$. Then 

\[  \det (\operatorname {sub}_P^Q(\operatorname {adj} A)) = (-1)^{\operatorname {sum} P + \operatorname {sum} Q} (\det A)^{|Q|-1} \det (\operatorname {sub}_{\widetilde{Q}}^{\widetilde{P}} A).  \]

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.mat.tilde
conv.mat.tilde

Let $n \in \mathbb {N}$. Let $A$ be an $n \times n$-matrix. Let $i, j \in [n]$. Then, we set 

\[  A_{\sim i, \sim j} := \operatorname {sub}_{[n] \setminus \{ i\} }^{[n] \setminus \{ j\} } A.  \]

 This is the $(n-1) \times (n-1)$-matrix obtained from $A$ by removing its $i$-th row and its $j$-th column.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.det.adj
Adjugate matrix

Let $n \in \mathbb {N}$. Let $A \in K^{n \times n}$ be an $n \times n$-matrix. We define a new $n \times n$-matrix $\operatorname {adj} A \in K^{n \times n}$ by 

\[  \operatorname {adj} A = \left( (-1)^{i+j} \det (A_{\sim j, \sim i}) \right)_{1 \leq i \leq n,\;  1 \leq j \leq n}.  \]

 This matrix $\operatorname {adj} A$ is called the \emph{adjugate} (or \emph{classical adjoint}) of the matrix $A$. Note the index swap: the $(i,j)$ entry involves removing row $j$ and column $i$. 

The formalization shows that this definition equals Mathlib’s \texttt{Matrix.adjugate}, which is defined via $(\operatorname {adj} A)_{i,j} = \det (A')$ where $A'$ is the matrix $A$ with row $j$ replaced by the $i$-th standard basis vector.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.det.det
def.det.det

Let $n \in \mathbb {N}$. Let $A \in K^{n \times n}$ be an $n \times n$-matrix. The \emph{determinant} $\det A$ of $A$ is defined to be the element 

\[  \sum _{\sigma \in S_n} (-1)^{\sigma } \underbrace{A_{1,\sigma (1)} A_{2,\sigma (2)} \cdots A_{n,\sigma (n)}}_{ = \prod _{i=1}^{n} A_{i,\sigma (i)}}  \]

 of $K$. Here: 

\begin{itemize} \item we let $S_n$ denote the $n$-th symmetric group (i.e., the group of permutations of $[n] = \{ 1, 2, \ldots , n\} $); 

\item we let $(-1)^{\sigma }$ denote the sign of the permutation $\sigma $ (as defined in Definition~ \ref{def.perm.sign}). 

\end{itemize}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.det.sub
def.det.sub

Let $n,m\in \mathbb {N}$. Let $A$ be an $n\times m$-matrix. 

Let $U$ be a subset of $[n]$. Let $V$ be a subset of $[m]$. 

Writing the two sets $U$ and $V$ as 

\[  U=\{ u_1,u_2,\ldots ,u_p\}  \quad \text{and}\quad V=\{ v_1,v_2,\ldots ,v_q\}   \]

 with 

\[  u_1<u_2<\cdots <u_p \quad \text{and}\quad v_1<v_2<\cdots <v_q,  \]

 we set 

\[  \operatorname {sub}_U^V A:=\left(A_{u_i,v_j}\right)_{1\le i\le p,\  1\le j\le q}.  \]

Roughly speaking, $\operatorname {sub}_U^V A$ is the matrix obtained from $A$ by focusing only on the $i$-th rows for $i\in U$ (that is, removing all the other rows) and only on the $j$-th columns for $j\in V$ (that is, removing all the other columns). 

This matrix $\operatorname {sub}_U^V A$ is called the \emph{submatrix of} $A$ \emph{obtained by restricting to the $U$-rows and the $V$-columns}. If this matrix is square (i.e., if $|U|=|V|$), then its determinant $\det (\operatorname {sub}_U^V A)$ is called a \emph{minor} of $A$.

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
  "verdict": "faithful",
  "justification": "The elaborated binders exactly encode the blueprint hypotheses: `[inst : Field K]`, `A : Matrix (Fin m) (Fin m) K`, `A.det \u2260 0`, `P Q : Finset (Fin m)`, `hPQ : P.card = Q.card`, and `P.card \u2265 1` correspond to \u201cLet K be a field,\u201d \u201cA \u2208 K^{m\u00d7m} with det A \u2260 0,\u201d and \u201cP,Q \u2286 [m] with |P|=|Q|\u22651.\u201d The order-preserving `finsetOrderEmb` maps implement the increasing-order submatrices from `def.det.sub`; the left side uses P as rows and Q as columns, while the complementary term uses Q\u1d9c as rows and P\u1d9c as columns, exactly as `sub_P^Q` and `sub_{Q\u0303}^{P\u0303}` require. The conclusion has the same factors and exponent `A.det ^ (Q.card - 1)`. Although `Fin m` is zero-based and the blueprint\u2019s `[m]` is one-based, replacing each index by one more changes `sum P + sum Q` by `P.card + Q.card = 2\u00b7P.card`, an even number, so the factor `(-1)^(sum P + sum Q)` is unchanged. Mathlib\u2019s `Matrix.adjugate` is also explicitly identified with the blueprint adjugate in the informal definition."
}