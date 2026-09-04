## TARGET AlgebraicCombinatorics.SymmetricPolynomials.permAction_id (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {N : ℕ} (f : AlgebraicCombinatorics.SymmetricPolynomials.P K N),
  AlgebraicCombinatorics.SymmetricPolynomials.permAction 1 f = f

Docstring: The identity permutation acts trivially (Proposition prop.sf.SN-acts (a)).
Label: prop.sf.SN-acts 

## TARGET AlgebraicCombinatorics.SymmetricPolynomials.permAction_mul (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {N : ℕ} (σ τ : Equiv.Perm (Fin N))
  (f : AlgebraicCombinatorics.SymmetricPolynomials.P K N),
  AlgebraicCombinatorics.SymmetricPolynomials.permAction (σ * τ) f =
    AlgebraicCombinatorics.SymmetricPolynomials.permAction σ
      (AlgebraicCombinatorics.SymmetricPolynomials.permAction τ f)

Docstring: Composition of permutation actions (Proposition prop.sf.SN-acts (b)).
Label: prop.sf.SN-acts 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P (def)
(K : Type u_2) → [CommRing K] → ℕ → Type u_2

Body:
fun K [CommRing K] N => MvPolynomial (Fin N) K

Docstring: The polynomial ring in N variables over K.
This corresponds to 𝒫 in the source (Definition def.sf.PS (a)).
Label: def.sf.PS 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.permAction (def)
{K : Type u_1} →
  [inst : CommRing K] →
    {N : ℕ} →
      Equiv.Perm (Fin N) →
        AlgebraicCombinatorics.SymmetricPolynomials.P K N → AlgebraicCombinatorics.SymmetricPolynomials.P K N

Body:
fun {K} [CommRing K] {N} σ f => (MvPolynomial.rename ⇑σ) f

Docstring: The action of a permutation on a polynomial by renaming variables.
This is σ · f = f[x_{σ(1)}, ..., x_{σ(N)}] in the source.
Label: def.sf.PS 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Body:
fun α => α ≃ α

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF One
Type u → Type u

Docstring: A type with a "one" element. 

## BASE-LIBRARY REF One.one
{α : Type u} → [self : One α] → α

Body:
fun α [self : One α] => self.1

Docstring: The "one" element of the type. 

## BASE-LIBRARY REF Equiv.Perm.instOne
{α : Type u_4} → One (Equiv.Perm α)

Body:
fun {α} => { one := Equiv.refl α }

Characterization: `(1 : Perm α)` is the identity permutation (`Equiv.Perm.coe_one`).

## BASE-LIBRARY REF Equiv.refl
(α : Sort u_1) → α ≃ α

Body:
fun α => { toFun := id, invFun := id, left_inv := ⋯, right_inv := ⋯ }

Docstring: Any type is equivalent to itself. 

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

## BASE-LIBRARY REF MvPolynomial
Type u_1 → (R : Type u_2) → [CommSemiring R] → Type (max u_2 u_1)

Body:
fun σ R [CommSemiring R] => AddMonoidAlgebra R (σ →₀ ℕ)

Docstring: Multivariate polynomial, where `σ` is the index set of the variables and
`R` is the coefficient ring 

## BASE-LIBRARY REF CommRing.mul_comm
∀ {α : Type u} [self : CommRing α] (a b : α), a * b = b * a

Docstring: Multiplication is commutative in a commutative multiplicative magma. 

## BASE-LIBRARY REF AlgHom
(R : Type u) →
  (A : Type v) →
    (B : Type w) →
      [inst : CommSemiring R] →
        [inst_1 : Semiring A] → [inst_2 : Semiring B] → [Algebra R A] → [Algebra R B] → Type (max v w)

Docstring: Defining the homomorphism in the category R-Alg, denoted `A →ₐ[R] B`. 

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF MvPolynomial.commSemiring
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → CommSemiring (MvPolynomial σ R)

Body:
fun {R} {σ} [CommSemiring R] => AddMonoidAlgebra.commSemiring

## BASE-LIBRARY REF AddMonoidAlgebra.commSemiring
{R : Type u_1} → {M : Type u_4} → [inst : CommSemiring R] → [AddCommMonoid M] → CommSemiring (AddMonoidAlgebra R M)

Body:
fun {R} {M} [CommSemiring R] [AddCommMonoid M] => { toSemiring := AddMonoidAlgebra.semiring, mul_comm := ⋯ }

## BASE-LIBRARY REF Finsupp
Type u_9 → (M : Type u_10) → [Zero M] → Type (max u_10 u_9)

Docstring: `Finsupp α M`, denoted `α →₀ M`, is the type of functions `f : α → M` such that
`f x = 0` for all but finitely many `x`. 

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

Body:
{ toMul := instMulNat, toZero := Nat.instAddMonoid.toAddZeroClass.toZero, zero_mul := Nat.zero_mul,
  mul_zero := Nat.mul_zero }

## BASE-LIBRARY REF Finsupp.instAddCommMonoid
{ι : Type u_1} → {M : Type u_3} → [inst : AddCommMonoid M] → AddCommMonoid (ι →₀ M)

Body:
fun {ι} {M} [AddCommMonoid M] => { toAddMonoid := Finsupp.instAddMonoid, add_comm := ⋯ }

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

Body:
inferInstance

## BASE-LIBRARY REF MvPolynomial.algebra
{R : Type u} →
  {S₁ : Type v} →
    {σ : Type u_1} →
      [inst : CommSemiring R] → [inst_1 : CommSemiring S₁] → [Algebra R S₁] → Algebra R (MvPolynomial σ S₁)

Body:
fun {R} {S₁} {σ} [CommSemiring R] [CommSemiring S₁] [Algebra R S₁] => AddMonoidAlgebra.algebra

## BASE-LIBRARY REF Algebra
(R : Type u) → (A : Type v) → [CommSemiring R] → [Semiring A] → Type (max u v)

Docstring: An associative unital `R`-algebra is a semiring `A` equipped with a map into its center `R → A`.

See the implementation notes in this file for discussion of the details of this definition.


## BASE-LIBRARY REF AddMonoidAlgebra.algebra
{R : Type u_1} →
  {A : Type u_4} →
    {M : Type u_7} →
      [inst : CommSemiring R] →
        [inst_1 : Semiring A] → [Algebra R A] → [inst_3 : AddMonoid M] → Algebra R (AddMonoidAlgebra A M)

Body:
fun {R} {A} {M} [CommSemiring R] [Semiring A] [Algebra R A] [AddMonoid M] =>
  { toSMul := AddMonoidAlgebra.smulZeroClass.toSMul,
    algebraMap := AddMonoidAlgebra.singleZeroRingHom.comp (algebraMap R A), commutes' := ⋯, smul_def' := ⋯ }

Docstring: The instance `Algebra R R[M]` whenever we have `Algebra R R`.

In particular this provides the instance `Algebra R R[M]`. 

## BASE-LIBRARY REF Algebra.id
(R : Type u) → [inst : CommSemiring R] → Algebra R R

Docstring: The identity map inducing an `Algebra` structure. 

## BASE-LIBRARY REF AlgHom.funLike
{R : Type u} →
  {A : Type v} →
    {B : Type w} →
      [inst : CommSemiring R] →
        [inst_1 : Semiring A] →
          [inst_2 : Semiring B] → [inst_3 : Algebra R A] → [inst_4 : Algebra R B] → FunLike (A →ₐ[R] B) A B

Body:
fun {R} {A} {B} [CommSemiring R] [Semiring A] [Semiring B] [Algebra R A] [Algebra R B] =>
  { coe := fun f => (↑↑f.toRingHom).toFun, coe_injective' := ⋯ }

## BASE-LIBRARY REF Semiring
Type u → Type u

Docstring: A `Semiring` is a type with addition, multiplication, a `0` and a `1` where addition is
commutative and associative, multiplication is associative and left and right distributive over
addition, and `0` and `1` are additive and multiplicative identities. 

## BASE-LIBRARY REF AlgHom.funLike._proof_1
∀ {R : Type u_3} {A : Type u_1} {B : Type u_2} [inst : CommSemiring R] [inst_1 : Semiring A] [inst_2 : Semiring B]
  [inst_3 : Algebra R A] [inst_4 : Algebra R B] (f g : A →ₐ[R] B),
  (fun f => (↑↑f.toRingHom).toFun) f = (fun f => (↑↑f.toRingHom).toFun) g → f = g

## BASE-LIBRARY REF MvPolynomial.rename
{σ : Type u_1} →
  {τ : Type u_2} → {R : Type u_4} → [inst : CommSemiring R] → (σ → τ) → MvPolynomial σ R →ₐ[R] MvPolynomial τ R

Body:
fun {σ} {τ} {R} [CommSemiring R] f => MvPolynomial.aeval (MvPolynomial.X ∘ f)

Docstring: Rename all the variables in a multivariable polynomial. 

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

## INFORMAL STATEMENT
prop.sf.SN-acts

The action of $S_N$ on $\mathcal{P}$ is a well-defined group action. In other words, the following holds: \medskip 

\textbf{(a)} We have $\operatorname {id}_{[N]} \cdot f = f$ for every $f \in \mathcal{P}$. \medskip 

\textbf{(b)} We have $(\sigma \tau ) \cdot f = \sigma \cdot (\tau \cdot f)$ for every $\sigma , \tau \in S_N$ and $f \in \mathcal{P}$.

## VERDICT
{
  "verdict": "faithful",
  "discrepancies": [],
  "justification": "The two formal theorems exactly certify the two group-action laws in the blueprint after unfolding `permAction`. For (a), the formal statement `permAction 1 f = f` matches \u201cid_[N] \u00b7 f = f\u201d; `(1 : Equiv.Perm (Fin N))` is the identity permutation. For (b), the formal statement `permAction (\u03c3 * \u03c4) f = permAction \u03c3 (permAction \u03c4 f)` matches \u201c(\u03c3\u03c4) \u00b7 f = \u03c3 \u00b7 (\u03c4 \u00b7 f)\u201d; permutation multiplication satisfies `(\u03c3 * \u03c4) x = \u03c3 (\u03c4 x)`, so the composition convention agrees. The definitions `P K N = MvPolynomial (Fin N) K` and `permAction \u03c3 f = MvPolynomial.rename \u21d1\u03c3 f` encode the polynomial ring and variable-renaming action. Using `Fin N` for `[N]` is a notational encoding, and quantifying over every commutative coefficient ring is more general than any fixed coefficient setting."
}