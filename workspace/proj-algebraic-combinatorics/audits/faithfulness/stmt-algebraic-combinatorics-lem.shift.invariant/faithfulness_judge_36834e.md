## TARGET AlgebraicCombinatorics.CauchyBinet.sign_decomposition_leftShift_invariant (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (P Q : Finset (Fin n)) (hcard : P.card = Q.card) (σ : Equiv.Perm (Fin n))
  (hσ : AlgebraicCombinatorics.CauchyBinet.imageFinset σ P = Q) (i : Fin n) (hi : ↑i + 1 < n) (hi_notP : i ∉ P)
  (hiplus_P : ⟨↑i + 1, hi⟩ ∈ P),
  let s := Equiv.swap i ⟨↑i + 1, hi⟩;
  let P' := AlgebraicCombinatorics.CauchyBinet.imageFinset s P;
  let σ' := σ * s;
  have hcard' := ⋯;
  have hσ' := ⋯;
  ↑(Equiv.Perm.sign σ') =
      (-1) ^ (AlgebraicCombinatorics.CauchyBinet.finsetSumFin P' + AlgebraicCombinatorics.CauchyBinet.finsetSumFin Q) *
          ↑(Equiv.Perm.sign (AlgebraicCombinatorics.CauchyBinet.extractAlpha P' Q hcard' σ' hσ')) *
        ↑(Equiv.Perm.sign (AlgebraicCombinatorics.CauchyBinet.extractBeta P' Q hcard' σ' hσ')) →
    ↑(Equiv.Perm.sign σ) =
      (-1) ^ (AlgebraicCombinatorics.CauchyBinet.finsetSumFin P + AlgebraicCombinatorics.CauchyBinet.finsetSumFin Q) *
          ↑(Equiv.Perm.sign (AlgebraicCombinatorics.CauchyBinet.extractAlpha P Q hcard σ hσ)) *
        ↑(Equiv.Perm.sign (AlgebraicCombinatorics.CauchyBinet.extractBeta P Q hcard σ hσ))

Docstring: The sign decomposition formula is preserved under left shifts.

This combines:
1. leftShift_preserves_combined_sign: (-1)^(sum P + sum Q) * sign(σ) is preserved
2. extractAlpha_leftShift_eq: sign(extractAlpha) is preserved
3. extractBeta_leftShift_eq: sign(extractBeta) is preserved

Together, these show that if the formula holds for (P', Q, σ'), it holds for (P, Q, σ). 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.imageFinset (def)
{n : ℕ} → Equiv.Perm (Fin n) → Finset (Fin n) → Finset (Fin n)

Body:
fun {n} σ P => Finset.map { toFun := ⇑σ, inj' := ⋯ } P

Docstring: The image of a finset under a permutation.

This is definitionally equal to `PermFinset.imageFinset` (see `imageFinset_eq_permFinset`).
New code should prefer `PermFinset.imageFinset`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.imageFinset_leftShift_eq (theorem)
∀ {n : ℕ} (P Q : Finset (Fin n)) (σ : Equiv.Perm (Fin n)),
  AlgebraicCombinatorics.CauchyBinet.imageFinset σ P = Q →
    ∀ (i : Fin n) (hi : ↑i + 1 < n),
      i ∉ P →
        ⟨↑i + 1, hi⟩ ∈ P →
          have s := Equiv.swap i ⟨↑i + 1, hi⟩;
          have P' := AlgebraicCombinatorics.CauchyBinet.imageFinset s P;
          have σ' := σ * s;
          AlgebraicCombinatorics.CauchyBinet.imageFinset σ' P' = Q

Docstring: Key lemma: After a left shift, Q' = Q (the image is preserved).

When we apply swap(i, i+1) to P (where i ∉ P, i+1 ∈ P) and compose σ with swap,
the image σ'(P') equals the original image Q.

This is because:
- For p ∈ P with p ≠ i+1: swap(p) = p, so σ'(swap(p)) = σ(swap(swap(p))) = σ(p)
- For p = i+1: swap(i+1) = i, so σ'(i) = σ(swap(i)) = σ(i+1)

Thus the multiset of images is unchanged. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.finsetSumFin (def)
{n : ℕ} → Finset (Fin n) → ℕ

Body:
fun {n} P => ∑ i ∈ P, ↑i

Docstring: Sum of elements in a finset of Fin n, viewed as natural numbers.
Used in the sign factor of the det(A+B) formula.

Note: This is named `finsetSumFin` to distinguish from `AlgebraicCombinatorics.QBinomialRec.finsetSumNat`,
which computes the sum of elements in a `Finset ℕ` directly.
Both compute "the sum of elements" but for different element types. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.extractAlpha (def)
{n : ℕ} →
  (P Q : Finset (Fin n)) →
    P.card = Q.card →
      (σ : Equiv.Perm (Fin n)) → AlgebraicCombinatorics.CauchyBinet.imageFinset σ P = Q → Equiv.Perm (Fin P.card)

Body:
fun {n} P Q hcard σ hσ =>
  let pEmb := P.orderEmbOfFin ⋯;
  have h := ⋯;
  let qIso := Q.orderIsoOfFin ⋯;
  let f := fun i => qIso.symm ⟨σ (pEmb i), ⋯⟩;
  have hf_inj := ⋯;
  have hf_surj := ⋯;
  Equiv.ofBijective f ⋯

Docstring: Extract α from σ: For σ with σ(P) = Q, extract the permutation α ∈ Perm(Fin |P|)
that describes how σ permutes the elements of P.

Specifically, if p₁ < p₂ < ... < pₖ are the elements of P and 
q₁ < q₂ < ... < qₖ are the elements of Q, then α is defined by
σ(pᵢ) = q_{α(i)}. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.extractBeta (def)
{n : ℕ} →
  (P Q : Finset (Fin n)) →
    P.card = Q.card →
      (σ : Equiv.Perm (Fin n)) → AlgebraicCombinatorics.CauchyBinet.imageFinset σ P = Q → Equiv.Perm (Fin Pᶜ.card)

Body:
fun {n} P Q hcard σ hσ =>
  have hcard' := ⋯;
  let pEmb := Pᶜ.orderEmbOfFin ⋯;
  have h := ⋯;
  let qIso := Qᶜ.orderIsoOfFin ⋯;
  let f := fun i => qIso.symm ⟨σ (pEmb i), ⋯⟩;
  have hf_inj := ⋯;
  have hf_surj := ⋯;
  Equiv.ofBijective f ⋯

Docstring: Extract β from σ: For σ with σ(P) = Q, extract the permutation β ∈ Perm(Fin |Pᶜ|)
that describes how σ permutes the elements of Pᶜ. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.submatrixOfFinset (def)
{R : Type u_1} →
  {n m : ℕ} →
    Matrix (Fin n) (Fin m) R → (U : Finset (Fin n)) → (V : Finset (Fin m)) → Matrix (Fin U.card) (Fin V.card) R

Body:
fun {R} {n m} A U V => A.submatrix ⇑(U.orderEmbOfFin ⋯) ⇑(V.orderEmbOfFin ⋯)

Docstring: The submatrix of A obtained by restricting to rows in U and columns in V.
This corresponds to `sub_U^V A` in the source (Definition def.det.sub).
Label: def.det.sub

## Mathematical Description

Let A be an n×m matrix. Let U ⊆ [n] and V ⊆ [m] be subsets.
Writing U = {u₁, u₂, ..., uₚ} with u₁ < u₂ < ... < uₚ
and V = {v₁, v₂, ..., vₚ} with v₁ < v₂ < ... < vₚ,
we define sub_U^V A := (A_{uᵢ,vⱼ})_{1≤i≤p, 1≤j≤q}.

This is the |U|×|V| matrix obtained from A by keeping only the rows
indexed by U and columns indexed by V, in increasing order.

## Terminology

- **Submatrix**: The matrix sub_U^V A
- **Minor**: When |U| = |V|, the determinant det(sub_U^V A) is called a minor of A
- **Principal minor**: When U = V, the minor det(sub_U^U A) is called a principal minor

## Implementation

In Mathlib, `Matrix.submatrix` takes functions for row and column selection.
For finite sets, we use the canonical order-preserving embedding `orderEmbOfFin`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.sigma_orderEmb_mem_of_imageFinset (theorem)
∀ {n : ℕ} (P Q : Finset (Fin n)) (σ : Equiv.Perm (Fin n)),
  AlgebraicCombinatorics.CauchyBinet.imageFinset σ P = Q → ∀ (i : Fin P.card), σ ((P.orderEmbOfFin ⋯) i) ∈ Q

Docstring: For σ with σ(P) = Q, the image of any element of P under σ lies in Q. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.submatrixDet (def)
{R : Type u_1} → [CommRing R] → {n : ℕ} → Matrix (Fin n) (Fin n) R → (P Q : Finset (Fin n)) → P.card = Q.card → R

Body:
fun {R} [CommRing R] {n} A P Q h => (A.submatrix ⇑(P.orderEmbOfFin ⋯) ⇑(Q.orderEmbOfFin ⋯)).det

Docstring: Helper: Given P, Q with same cardinality, compute the determinant of the
submatrix of A restricted to rows P and columns Q. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.sigma_orderEmb_compl_mem_of_imageFinset (theorem)
∀ {n : ℕ} (P Q : Finset (Fin n)) (σ : Equiv.Perm (Fin n)),
  AlgebraicCombinatorics.CauchyBinet.imageFinset σ P = Q → ∀ (i : Fin Pᶜ.card), σ ((Pᶜ.orderEmbOfFin ⋯) i) ∈ Qᶜ

Docstring: For σ with σ(P) = Q, the image of any element of Pᶜ under σ lies in Qᶜ. 

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Body:
fun {α} s => s.val.card

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Body:
fun α => α ≃ α

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF Nat.lt
ℕ → ℕ → Prop

Body:
fun n m => n.succ.le m

Docstring: Strict inequality of natural numbers, usually accessed via the `<` operator.

It is defined as `n < m = n + 1 ≤ m`.


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


## BASE-LIBRARY REF Multiset
Type u → Type u

Body:
fun α => Quotient (List.isSetoid α)

Docstring: `Multiset α` is the quotient of `List α` by list permutation. The result
is a type of finite sets with duplicates allowed. 

## BASE-LIBRARY REF Finset.val
{α : Type u_4} → Finset α → Multiset α

Body:
fun α self => self.1

Docstring: The underlying multiset 

## BASE-LIBRARY REF Equiv.swap
{α : Sort u_1} → [DecidableEq α] → α → α → Equiv.Perm α

Body:
fun {α} [DecidableEq α] a b =>
  { toFun := Equiv.swapCore a b, invFun := Equiv.swapCore a b, left_inv := ⋯, right_inv := ⋯ }

Docstring: `swap a b` is the permutation that swaps `a` and `b` and
leaves other values as is. 

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

## BASE-LIBRARY REF Mul
Type u → Type u

Docstring: The homogeneous version of `HMul`: `a * b : α` where `a b : α`. 

## BASE-LIBRARY REF Mul.mul
{α : Type u} → [self : Mul α] → α → α → α

Body:
fun α [self : Mul α] => self.1

Docstring: `a * b` computes the product of `a` and `b`. See `HMul`. 

## BASE-LIBRARY REF Equiv.Perm.instMul
{α : Type u_4} → Mul (Equiv.Perm α)

Body:
fun {α} => { mul := fun f g => Equiv.trans g f }

Characterization: `(σ * τ) x = σ (τ x)`: multiplication is composition, right factor first (`Equiv.Perm.coe_mul`).

## BASE-LIBRARY REF Equiv.trans
{α : Sort u} → {β : Sort v} → {γ : Sort w} → α ≃ β → β ≃ γ → α ≃ γ

Body:
fun {α} {β} {γ} e₁ e₂ => { toFun := ⇑e₂ ∘ ⇑e₁, invFun := ⇑e₁.symm ∘ ⇑e₂.symm, left_inv := ⋯, right_inv := ⋯ }

Docstring: Composition of equivalences `e₁ : α ≃ β` and `e₂ : β ≃ γ`. 

## BASE-LIBRARY REF Eq.mpr
{α β : Sort u} → α = β → β → α

Body:
fun {α β} h b => ⋯ ▸ b

Docstring: If `h : α = β` is a proof of type equality, then `h.mpr : β → α` is the induced
"cast" operation in the reverse direction, mapping elements of `β` to elements of `α`.

You can prove theorems about the resulting element by induction on `h`, since
`rfl.mpr` is definitionally the identity function.


## BASE-LIBRARY REF congrFun'
∀ {α : Sort u} {β : Sort v} {f g : α → β}, f = g → ∀ (a : α), f a = g a

Docstring: Similar to `congrFun` but `β` does not depend on `α`. 

## BASE-LIBRARY REF congrArg
∀ {α : Sort u} {β : Sort v} {a₁ a₂ : α} (f : α → β), a₁ = a₂ → f a₁ = f a₂

Docstring: Congruence in the function argument: if `a₁ = a₂` then `f a₁ = f a₂` for
any (nondependent) function `f`. This is more powerful than it might look at first, because
you can also use a lambda expression for `f` to prove that
`<something containing a₁> = <something containing a₂>`. This function is used
internally by tactics like `congr` and `simp` to apply equalities inside
subterms.

For more information: [Equality](https://lean-lang.org/theorem_proving_in_lean4/quantifiers_and_equality.html#equality)


## BASE-LIBRARY REF Finset.card_map
∀ {α : Type u_1} {β : Type u_2} {s : Finset α} (f : α ↪ β), (Finset.map f s).card = s.card

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

## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

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

## BASE-LIBRARY REF Units.val
{α : Type u} → [inst : Monoid α] → αˣ → α

Body:
fun α [Monoid α] self => self.1

Docstring: The underlying value in the base `Monoid`. 

Characterization: The coercion from the unit group to the monoid respects the operations: `↑(u * v) = ↑u * ↑v`, `↑u⁻¹ * ↑u = 1` (`Units.val_mul`, `Units.inv_mul`).

## BASE-LIBRARY REF Int.instMonoid
Monoid ℤ

Body:
inferInstance

## BASE-LIBRARY REF Monoid
Type u → Type u

Docstring: A `Monoid` is a `Semigroup` with an element `1` such that `1 * a = a * 1 = a`. 

## BASE-LIBRARY REF Int.instCommMonoid
CommMonoid ℤ

Body:
{ toMul := Int.instMul, mul_assoc := Int.mul_assoc, toOne := One.ofOfNat1, one_mul := Int.one_mul,
  mul_one := Int.mul_one, npow := fun n x => x ^ n, npow_zero := ⋯, npow_succ := ⋯, mul_comm := Int.mul_comm }

## BASE-LIBRARY REF MonoidHom
(M : Type u_10) → (N : Type u_11) → [MulOne M] → [MulOne N] → Type (max u_10 u_11)

Docstring: `M →* N` is the type of functions `M → N` that preserve the `MulOne` structure.
`MonoidHom` is used for both monoid and group homomorphisms.

When possible, instead of parametrizing results over `(f : M →* N)`,
you should parametrize over `(F : Type*) [MonoidHomClass F M N] (f : F)`.

When you extend this structure, make sure to extend `MonoidHomClass`.


## BASE-LIBRARY REF Units
(α : Type u) → [Monoid α] → Type u

Docstring: Units of a `Monoid`, bundled version. Notation: `αˣ`.

An element of a `Monoid` is a unit if it has a two-sided inverse.
This version bundles the inverse element so that it can be computed.
For a predicate see `IsUnit`. 

## BASE-LIBRARY REF MulOneClass
Type u → Type u

Docstring: Typeclass for expressing that a type `M` with multiplication and a one satisfies
`1 * a = a` and `a * 1 = a` for all `a : M`. 

## BASE-LIBRARY REF Monoid.one_mul
∀ {M : Type u} [self : Monoid M] (a : M), 1 * a = a

Docstring: One is a left neutral element for multiplication 

## BASE-LIBRARY REF Monoid.mul_one
∀ {M : Type u} [self : Monoid M] (a : M), a * 1 = a

Docstring: One is a right neutral element for multiplication 

## BASE-LIBRARY REF DivInvMonoid
Type u → Type u

Docstring: A `DivInvMonoid` is a `Monoid` with operations `/` and `⁻¹` satisfying
`div_eq_mul_inv : ∀ a b, a / b = a * b⁻¹`.

This deduplicates the name `div_eq_mul_inv`.
The default for `div` is such that `a / b = a * b⁻¹` holds by definition.

Adding `div` as a field rather than defining `a / b := a * b⁻¹` allows us to
avoid certain classes of unification failures, for example:
Let `Foo X` be a type with a `∀ X, Div (Foo X)` instance but no
`∀ X, Inv (Foo X)`, e.g. when `Foo X` is a `EuclideanDomain`. Suppose we
also have an instance `∀ X [Cromulent X], GroupWithZero (Foo X)`. Then the
`(/)` coming from `GroupWithZero.div` cannot be definitionally equal to
the `(/)` coming from `Foo.Div`.

In the same way, adding a `zpow` field makes it possible to avoid definitional failures
in diamonds. See the definition of `Monoid` and Note [forgetful inheritance] for more
explanations on this.


## BASE-LIBRARY REF Group
Type u → Type u

Docstring: A `Group` is a `Monoid` with an operation `⁻¹` satisfying `a⁻¹ * a = 1`.

There is also a division operation `/` such that `a / b = a * b⁻¹`,
with a default so that `a / b = a * b⁻¹` holds by definition.

Use `Group.ofLeftAxioms` or `Group.ofRightAxioms` to define a group structure
on a type with the minimum proof obligations.


## BASE-LIBRARY REF Equiv.Perm.permGroup
{α : Type u_4} → Group (Equiv.Perm α)

Body:
fun {α} =>
  { toMul := Equiv.Perm.instMul, mul_assoc := ⋯, toOne := Equiv.Perm.instOne, one_mul := ⋯, mul_one := ⋯,
    npow := fun n f => f ^ n, npow_zero := ⋯, npow_succ := ⋯, toInv := Equiv.Perm.instInv, div := DivInvMonoid.div',
    div_eq_mul_inv := ⋯, zpow := zpowRec fun n f => f ^ n, zpow_zero' := ⋯, zpow_succ' := ⋯, zpow_neg' := ⋯,
    inv_mul_cancel := ⋯ }

## BASE-LIBRARY REF Equiv.Perm.permGroup._proof_5
∀ {α : Type u_1} (x x_1 x_2 : Equiv.Perm α), Equiv.trans x_2 (Equiv.trans x_1 x) = (Equiv.trans x_2 x_1).trans x

## BASE-LIBRARY REF Equiv.Perm.instOne
{α : Type u_4} → One (Equiv.Perm α)

Body:
fun {α} => { one := Equiv.refl α }

Characterization: `(1 : Perm α)` is the identity permutation (`Equiv.Perm.coe_one`).

## BASE-LIBRARY REF Equiv.trans_refl
∀ {α : Sort u} {β : Sort v} (e : α ≃ β), e.trans (Equiv.refl β) = e

## BASE-LIBRARY REF Equiv.refl_trans
∀ {α : Sort u} {β : Sort v} (e : α ≃ β), (Equiv.refl α).trans e = e

## BASE-LIBRARY REF Equiv.Perm.instPowNat
{α : Type u_4} → Pow (Equiv.Perm α) ℕ

Body:
fun {α} => { pow := fun f n => { toFun := (⇑f)^[n], invFun := (⇑(Equiv.symm f))^[n], left_inv := ⋯, right_inv := ⋯ } }

## BASE-LIBRARY REF Equiv.Perm.permGroup._proof_1
∀ {α : Type u_1} (x : Equiv.Perm α), x ^ 0 = 1

## BASE-LIBRARY REF Units.instMulOneClass
{α : Type u} → [inst : Monoid α] → MulOneClass αˣ

Body:
fun {α} [Monoid α] => { toOne := Units.instOne, toMul := Units.instMul, one_mul := ⋯, mul_one := ⋯ }

Docstring: Units of a monoid have a multiplication and multiplicative identity. 

## BASE-LIBRARY REF MonoidHom.instFunLike
{M : Type u_4} → {N : Type u_5} → [inst : MulOne M] → [inst_1 : MulOne N] → FunLike (M →* N) M N

Body:
fun {M} {N} [MulOne M] [MulOne N] => { coe := fun f => (↑f).toFun, coe_injective' := ⋯ }

## BASE-LIBRARY REF MulOne
Type u_2 → Type u_2

Docstring: Bundling a `Mul` and `One` structure together without any axioms about their
compatibility. See `MulOneClass` for the additional assumption that 1 is an identity. 

## BASE-LIBRARY REF MonoidHom.instFunLike._proof_1
∀ {M : Type u_1} {N : Type u_2} [inst : MulOne M] [inst_1 : MulOne N] (f g : M →* N),
  (fun f => (↑f).toFun) f = (fun f => (↑f).toFun) g → f = g

## BASE-LIBRARY REF Equiv.Perm.sign
{α : Type u} → [DecidableEq α] → [Fintype α] → Equiv.Perm α →* ℤˣ

Body:
fun {α} [DecidableEq α] [Fintype α] => MonoidHom.mk' (fun f => f.signAux3 ⋯) ⋯

Docstring: `SignType.sign` of a permutation returns the signature or parity of a permutation, `1` for even
permutations, `-1` for odd permutations. It is the unique surjective group homomorphism from
`Perm α` to the group with two elements. 

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

## BASE-LIBRARY REF Int.instMul
Mul ℤ

Body:
{ mul := Int.mul }

## BASE-LIBRARY REF Int.mul
ℤ → ℤ → ℤ

Body:
fun m n =>
  match m, n with
  | Int.ofNat m, Int.ofNat n => Int.ofNat (m * n)
  | Int.ofNat m, Int.negSucc n => Int.negOfNat (m * n.succ)
  | Int.negSucc m, Int.ofNat n => Int.negOfNat (m.succ * n)
  | Int.negSucc m, Int.negSucc n => Int.ofNat (m.succ * n.succ)

Docstring: Multiplication of integers, usually accessed via the `*` operator.

This function is overridden by the compiler with an efficient implementation. This definition is
the logical model.

Examples:
 * `(63 : Int) * (6 : Int) = 378`
 * `(6 : Int) * (-6 : Int) = -36`
 * `(7 : Int) * (0 : Int) = 0`


## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Body:
fun α [self : Neg α] => self.1

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF Int.instNegInt
Neg ℤ

Body:
{ neg := Int.neg }

## BASE-LIBRARY REF Int.neg
ℤ → ℤ

Body:
fun n =>
  match n with
  | Int.ofNat n => Int.negOfNat n
  | Int.negSucc n => ↑n.succ

Docstring: Negation of integers, usually accessed via the `-` prefix operator.

This function is overridden by the compiler with an efficient implementation. This definition is
the logical model.

Examples:
 * `-(6 : Int) = -6`
 * `-(-6 : Int) = 6`
 * `(12 : Int).neg = -12`


## BASE-LIBRARY REF Int.ofNat
ℕ → ℤ

Docstring: A natural number is an integer.

This constructor covers the non-negative integers (from `0` to `∞`).


## BASE-LIBRARY REF Compl.compl
{α : Type u_1} → [self : Compl α] → α → α

Body:
fun α [self : Compl α] => self.1

Docstring: Set / lattice complement 

Conventions for notations in identifiers:

 * The recommended spelling of `ᶜ` in identifiers is `compl`.

## BASE-LIBRARY REF BooleanAlgebra
Type u → Type u

Docstring: A Boolean algebra is a bounded distributive lattice with a complement operator `ᶜ` such that
`x ⊓ xᶜ = ⊥` and `x ⊔ xᶜ = ⊤`. For convenience, it must also provide a set difference operation `\`
and a Heyting implication `⇨` satisfying `x \ y = x ⊓ yᶜ` and `x ⇨ y = y ⊔ xᶜ`.

This is a generalization of (classical) logic of propositions, or the powerset lattice.

Since `BoundedOrder`, `OrderBot`, and `OrderTop` are mixins that require `LE`
to be present at define-time, the `extends` mechanism does not work with them.
Instead, we extend using the underlying `Bot` and `Top` data typeclasses, and replicate the
order axioms of those classes here. A "forgetful" instance back to `BoundedOrder` is provided.


## BASE-LIBRARY REF Finset.booleanAlgebra
{α : Type u_1} → [Fintype α] → [DecidableEq α] → BooleanAlgebra (Finset α)

Body:
fun {α} [Fintype α] [DecidableEq α] => GeneralizedBooleanAlgebra.toBooleanAlgebra

## BASE-LIBRARY REF Fintype
Type u_4 → Type u_4

Docstring: `Fintype α` means that `α` is finite, i.e. there are only
finitely many distinct elements of type `α`. The evidence of this
is a finset `elems` (a list up to permutation without duplicates),
together with a proof that everything of type `α` is in the list. 

## BASE-LIBRARY REF Finset.instGeneralizedBooleanAlgebra
{α : Type u_1} → [DecidableEq α] → GeneralizedBooleanAlgebra (Finset α)

Body:
fun {α} [DecidableEq α] =>
  { toDistribLattice := Finset.instDistribLattice, toSDiff := Finset.instSDiff, toBot := Finset.instOrderBot.toBot,
    sup_inf_sdiff := ⋯, inf_inf_sdiff := ⋯ }

## BASE-LIBRARY REF Finset.boundedOrder
{α : Type u_1} → [Fintype α] → BoundedOrder (Finset α)

Body:
fun {α} [Fintype α] =>
  have __src := inferInstanceAs (OrderBot (Finset α));
  { top := Finset.univ, le_top := ⋯, toOrderBot := __src }

## BASE-LIBRARY REF Finset.map
{α : Type u_1} → {β : Type u_2} → (α ↪ β) → Finset α → Finset β

Body:
fun {α} {β} f s => { val := Multiset.map (⇑f) s.val, nodup := ⋯ }

Docstring: When `f` is an embedding of `α` in `β` and `s` is a finset in `α`, then `s.map f` is the image
finset in `β`. The embedding condition guarantees that there are no duplicates in the image. 

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Body:
fun {ι} {M} [AddCommMonoid M] s f => (Multiset.map f s.val).sum

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

Body:
inferInstance

## BASE-LIBRARY REF AddCommMonoid
Type u → Type u

Docstring: An additive commutative monoid is an additive monoid with commutative `(+)`. 

## BASE-LIBRARY REF Nat.instAddCancelCommMonoid
AddCancelCommMonoid ℕ

Body:
{ add := Nat.add, add_assoc := Nat.add_assoc, zero := Nat.zero, zero_add := Nat.zero_add, add_zero := Nat.add_zero,
  nsmul := fun m n => m * n, nsmul_zero := Nat.zero_mul, nsmul_succ := Nat.succ_mul, add_comm := Nat.add_comm,
  toIsLeftCancelAdd := Nat.instAddCancelCommMonoid._proof_1 }

## BASE-LIBRARY REF OrderEmbedding
(α : Type u_6) → (β : Type u_7) → [LE α] → [LE β] → Type (max u_6 u_7)

Body:
fun α β [LE α] [LE β] => (fun x1 x2 => x1 ≤ x2) ↪r fun x1 x2 => x1 ≤ x2

Docstring: An order embedding is an embedding `f : α ↪ β` such that `a ≤ b ↔ (f a) ≤ (f b)`.
This definition is an abbreviation of `RelEmbedding (≤) (≤)`. 

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

## BASE-LIBRARY REF Finset.orderEmbOfFin
{α : Type u_1} → [inst : LinearOrder α] → (s : Finset α) → {k : ℕ} → s.card = k → Fin k ↪o α

Body:
fun {α} [LinearOrder α] s {k} h =>
  RelEmbedding.trans (s.orderIsoOfFin h).toOrderEmbedding (OrderEmbedding.subtype fun x => x ∈ s)

Docstring: Given a finset `s` of cardinality `k` in a linear order `α`, the map `orderEmbOfFin s h` is
the increasing bijection between `Fin k` and `s` as an order embedding into `α`. Here, `h` is a
proof that the cardinality of `s` is `k`. We use this instead of an embedding `Fin s.card ↪o α` to
avoid casting issues in further uses of this function. 

## BASE-LIBRARY REF LE
Type u → Type u

Docstring: `LE α` is the typeclass which supports the notation `x ≤ y` where `x y : α`.

## BASE-LIBRARY REF RelEmbedding.instFunLike
{α : Type u_1} → {β : Type u_2} → {r : α → α → Prop} → {s : β → β → Prop} → FunLike (r ↪r s) α β

Body:
fun {α} {β} {r} {s} => { coe := fun x => x.toFun, coe_injective' := ⋯ }

## BASE-LIBRARY REF OrderIso
(α : Type u_6) → (β : Type u_7) → [LE α] → [LE β] → Type (max u_6 u_7)

Body:
fun α β [LE α] [LE β] => (fun x1 x2 => x1 ≤ x2) ≃r fun x1 x2 => x1 ≤ x2

Docstring: An order isomorphism is an equivalence such that `a ≤ b ↔ (f a) ≤ (f b)`.
This definition is an abbreviation of `RelIso (≤) (≤)`. 

## BASE-LIBRARY REF SetLike
Type u_1 → outParam (Type u_2) → Type (max u_1 u_2)

Docstring: A class to indicate that there is a canonical injection between `A` and `Set B`.

This has the effect of giving terms of `A` elements of type `B` (through a `Membership`
instance) and a compatible coercion to `Type*` as a subtype.

Note: if `SetLike.coe` is a projection, implementers should create a simp lemma such as
```
@[simp] lemma mem_carrier {p : MySubobject X} : x ∈ p.carrier ↔ x ∈ (p : Set X) := Iff.rfl
```
to normalize terms.

If you declare an unbundled subclass of `SetLike`, for example:
```
class MulMemClass (S : Type*) (M : Type*) [Mul M] [SetLike S M] where
  ...
```
Then you should *not* repeat the `outParam` declaration so `SetLike` will supply the value instead.
This ensures your subclass will not have issues with synthesis of the `[Mul M]` parameter starting
before the value of `M` is known.


## BASE-LIBRARY REF SetLike.coe
{A : Type u_1} → {B : outParam (Type u_2)} → [self : SetLike A B] → A → Set B

Body:
fun A {B} [self : SetLike A B] => self.1

Docstring: The coercion from a term of a `SetLike` to its corresponding `Set`. 

## BASE-LIBRARY REF Finset.instSetLike
{α : Type u_1} → SetLike (Finset α) α

Body:
fun {α} => { coe := fun s => {a | a ∈ s}, coe_injective' := ⋯ }

Docstring: Convert a finset to a set in the natural way. 

## BASE-LIBRARY REF Subtype.instLE
{α : Type u} → [LE α] → {P : α → Prop} → LE (Subtype P)

Body:
fun {α} [LE α] {P} => { le := fun a b => ↑a ≤ ↑b }

## BASE-LIBRARY REF Finset.orderIsoOfFin
{α : Type u_1} → [inst : LinearOrder α] → (s : Finset α) → {k : ℕ} → s.card = k → Fin k ≃o ↥s

Body:
fun {α} [LinearOrder α] s {k} h =>
  (Fin.castOrderIso ⋯).trans
    ((List.SortedLT.getIso (s.sort fun a b => a ≤ b) ⋯).trans
      (OrderIso.setCongr (fun x => List.Mem x (s.sort fun a b => a ≤ b)) ↑s ⋯))

Docstring: Given a finset `s` of cardinality `k` in a linear order `α`, the map `orderIsoOfFin s h`
is the increasing bijection between `Fin k` and `s` as an `OrderIso`. Here, `h` is a proof that
the cardinality of `s` is `k`. We use this instead of an iso `Fin s.card ≃o s` to avoid
casting issues in further uses of this function. 

## BASE-LIBRARY REF RelIso.instFunLike
{α : Type u_1} → {β : Type u_2} → {r : α → α → Prop} → {s : β → β → Prop} → FunLike (r ≃r s) α β

Body:
fun {α} {β} {r} {s} => { coe := fun x => ⇑x.toRelEmbedding, coe_injective' := ⋯ }

## BASE-LIBRARY REF OrderIso.symm
{α : Type u_2} → {β : Type u_3} → [inst : LE α] → [inst_1 : LE β] → α ≃o β → β ≃o α

Body:
fun {α} {β} [LE α] [LE β] e => RelIso.symm e

Docstring: Inverse of an order isomorphism. 

## BASE-LIBRARY REF Function.Injective
{α : Sort u_1} → {β : Sort u_2} → (α → β) → Prop

Body:
fun {α} {β} f => ∀ ⦃a₁ a₂ : α⦄, f a₁ = f a₂ → a₁ = a₂

Docstring: A function `f : α → β` is called injective if `f x = f y` implies `x = y`. 

## BASE-LIBRARY REF Function.Surjective
{α : Sort u_1} → {β : Sort u_2} → (α → β) → Prop

Body:
fun {α} {β} f => ∀ (b : β), ∃ a, f a = b

Docstring: A function `f : α → β` is called surjective if every `b : β` is equal to `f a`
for some `a : α`. 

## BASE-LIBRARY REF Equiv.ofBijective
{α : Sort u} → {β : Sort v} → (f : α → β) → Function.Bijective f → α ≃ β

Body:
fun {α} {β} f hf => { toFun := f, invFun := Function.surjInv ⋯, left_inv := ⋯, right_inv := ⋯ }

Docstring: If `f` is a bijective function, then its domain is equivalent to its codomain. 

## BASE-LIBRARY REF Matrix
Type u → Type u' → Type v → Type (max u u' v)

Body:
fun m n α => m → n → α

Docstring: `Matrix m n R` is the type of matrices with entries in `R`, whose rows are indexed by `m`
and whose columns are indexed by `n`. 

## BASE-LIBRARY REF Matrix.submatrix
{l : Type u_1} →
  {m : Type u_2} → {n : Type u_3} → {o : Type u_4} → {α : Type v} → Matrix m n α → (l → m) → (o → n) → Matrix l o α

Body:
fun {l} {m} {n} {o} {α} A r c => Matrix.of fun i j => A (r i) (c j)

Docstring: Given maps `(r : l → m)` and `(c : o → n)` reindexing the rows and columns of
a matrix `M : Matrix m n α`, the matrix `M.submatrix r c : Matrix l o α` is defined
by `(M.submatrix r c) i j = M (r i) (c j)` for `(i,j) : l × o`.
Note that the total number of row and columns does not have to be preserved. 

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


## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Matrix.det
{n : Type u_2} → [DecidableEq n] → [Fintype n] → {R : Type v} → [CommRing R] → Matrix n n R → R

Body:
fun {n} [DecidableEq n] [Fintype n] {R} [CommRing R] M => Matrix.detRowAlternating M

Docstring: The determinant of a matrix given by the Leibniz formula. 

## INFORMAL STATEMENT
Left shift invariance

\leanhelper  If the sign decomposition formula holds for $(P', Q, \sigma ')$ (where $P' = s_i(P)$, $\sigma ' = \sigma \cdot s_i$), then it holds for $(P, Q, \sigma )$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv-2eb59533
conv-2eb59533

In the Lean formalization, we use $\operatorname {Fin} n = \{ 0, 1, \ldots , n-1\} $ instead of the textbook’s $[n] = \{ 1, 2, \ldots , n\} $. Both are $n$-element sets, so their symmetric groups are isomorphic. Permutations are represented by the type of bijections $X \to X$ (denoted $\operatorname {Equiv.Perm}\,  X$ in Lean), which is a group under composition. Composition $\alpha \beta $ is the group multiplication $\alpha * \beta $, sending $x$ to $\alpha (\beta (x))$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.det.imagefinset
def.det.imageFinset

\leanhelper  The \emph{image} of a finite subset $P \subseteq [n]$ under a permutation $\sigma \in S_n$ is $\sigma (P) = \{ \sigma (i) \mid i \in P\} $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## VERDICT
{
  "verdict": "faithful",
  "discrepancies": [],
  "justification": "The formal implication exactly matches the blueprint\u2019s direction: the hypothesis is the sign decomposition formula for `(P', Q, \u03c3')`, and the conclusion is the same formula for `(P, Q, \u03c3)`. The formal definitions agree with the parenthetical specification: `s := Equiv.swap i \u27e8\u2191i + 1, hi\u27e9`, `P' := imageFinset s P`, and `\u03c3' := \u03c3 * s`, matching \u201cwhere $P' = s_i(P)$, $\\sigma' = \\sigma \\cdot s_i$.\u201d The assumptions `i \u2209 P` and `\u27e8\u2191i + 1, hi\u27e9 \u2208 P` encode that this adjacent swap is a left shift, while `hcard : P.card = Q.card` and `h\u03c3 : imageFinset \u03c3 P = Q` are the domain conditions needed for the displayed sign decomposition and its extracted permutations. The supplied convention confirms that permutation multiplication sends `x` to `\u03c3 (s x)`, exactly as required."
}