## TARGET PowerSeries.prodRule_claim11 (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {I : Type u_2} [inst_1 : DecidableEq I] (p : I → ℕ → PowerSeries K) (In : Finset I)
  (S : I → Finset ℕ), ∏ i ∈ In, ∑ k ∈ S i, p i k = ∑ f ∈ Fintype.piFinset fun i => S ↑i, ∏ i, p (↑i) (f i)

Docstring: Claim 11: For finite `I_n`, `∏_{i ∈ I_n} ∑_{k ∈ S_i} p_{i,k} =
∑_{(k_i) ∈ S^{I_n}} ∏_{i ∈ I_n} p_{i,k_i}`.
(Claim 11) 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Body:
fun R => MvPowerSeries Unit R

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

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

## BASE-LIBRARY REF PowerSeries.instCommRing
{R : Type u_1} → [CommRing R] → CommRing (PowerSeries R)

Body:
fun {R} [CommRing R] => id inferInstance

## BASE-LIBRARY REF MvPowerSeries
Type u_1 → Type u_2 → Type (max (max u_2 0) u_1)

Body:
fun σ R => (σ →₀ ℕ) → R

Docstring: Multivariate formal power series, where `σ` is the index set of the variables
and `R` is the coefficient ring. 

## BASE-LIBRARY REF MvPowerSeries.instCommRing
{σ : Type u_1} → {R : Type u_2} → [CommRing R] → CommRing (MvPowerSeries σ R)

Body:
fun {σ} {R} [CommRing R] =>
  let __src := inferInstanceAs (CommSemiring (MvPowerSeries σ R));
  let __src_1 := inferInstanceAs (AddCommGroup (MvPowerSeries σ R));
  { toSemiring := __src.toSemiring, toNeg := __src_1.toNeg, toSub := __src_1.toSub, sub_eq_add_neg := ⋯,
    zsmul := SubNegMonoid.zsmul, zsmul_zero' := ⋯, zsmul_succ' := ⋯, zsmul_neg' := ⋯, neg_add_cancel := ⋯,
    toIntCast := MvPowerSeries.instRing.toAddGroupWithOne.toIntCast, intCast_ofNat := ⋯, intCast_negSucc := ⋯,
    mul_comm := ⋯ }

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Body:
fun {ι} {M} [AddCommMonoid M] s f => (Multiset.map f s.val).sum

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF PowerSeries.instAddCommMonoid
{R : Type u_1} → [AddCommMonoid R] → AddCommMonoid (PowerSeries R)

Body:
fun {R} [AddCommMonoid R] => id inferInstance

## BASE-LIBRARY REF AddCommMonoid
Type u → Type u

Docstring: An additive commutative monoid is an additive monoid with commutative `(+)`. 

## BASE-LIBRARY REF MvPowerSeries.instAddCommMonoid
{σ : Type u_1} → {R : Type u_2} → [AddCommMonoid R] → AddCommMonoid (MvPowerSeries σ R)

Body:
fun {σ} {R} [AddCommMonoid R] => Pi.addCommMonoid

## BASE-LIBRARY REF NonUnitalNonAssocSemiring
Type u → Type u

Docstring: A not-necessarily-unital, not-necessarily-associative semiring. See `CommutatorRing` and the
documentation thereof in case you need a `NonUnitalNonAssocSemiring` instance on a Lie ring
or a Lie algebra. 

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

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing._proof_1
∀ {α : Type u_1} [s : CommRing α] (a b : α), a - b = a + -b

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing._proof_2
∀ {α : Type u_1} [s : CommRing α] (a : α), Ring.zsmul 0 a = 0

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

## BASE-LIBRARY REF Fintype.piFinset
{α : Type u_1} → [DecidableEq α] → [Fintype α] → {δ : α → Type u_4} → ((a : α) → Finset (δ a)) → Finset ((a : α) → δ a)

Body:
fun {α} [DecidableEq α] [Fintype α] {δ} t => Finset.map { toFun := fun f a => f a ⋯, inj' := ⋯ } (Finset.univ.pi t)

Docstring: Given for all `a : α` a finset `t a` of `δ a`, then one can define the
finset `Fintype.piFinset t` of all functions taking values in `t a` for all `a`. This is the
analogue of `Finset.pi` where the base finset is `univ` (but formally they are not the same, as
there is an additional condition `i ∈ Finset.univ` in the `Finset.pi` definition). 

## BASE-LIBRARY REF Subtype.instDecidableEq.match_1
{α : Sort u_1} →
  {p : α → Prop} →
    (motive : { x // p x } → Sort u_2) → (x : { x // p x }) → ((b : α) → (h₂ : p b) → motive ⟨b, h₂⟩) → motive x

Body:
fun {α} {p} motive x h_1 => Subtype.casesOn x fun val property => h_1 val property

## BASE-LIBRARY REF dite
{α : Sort u} → (c : Prop) → [h : Decidable c] → (c → α) → (¬c → α) → α

Body:
fun {α} c [h : Decidable c] t e => Decidable.casesOn h e t

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


## BASE-LIBRARY REF Decidable.isTrue
{p : Prop} → p → Decidable p

Docstring: Proves that `p` is decidable by supplying a proof of `p` 

## BASE-LIBRARY REF Subtype.instDecidableEq._proof_3
∀ {α : Sort u_1} {p : α → Prop} (a : α) (h₁ : p a) (b : α) (h₂ : p b), a = b → ⟨a, h₁⟩ = ⟨b, h₂⟩

## BASE-LIBRARY REF Decidable.isFalse
{p : Prop} → ¬p → Decidable p

Docstring: Proves that `p` is decidable by supplying a proof of `¬p` 

## BASE-LIBRARY REF Subtype.instDecidableEq._proof_1
∀ {α : Sort u_1} {p : α → Prop} (a : α) (h₁ : p a) (b : α) (h₂ : p b), ¬a = b → ⟨a, h₁⟩ = ⟨b, h₂⟩ → False

## BASE-LIBRARY REF Finset.Subtype.fintype
{α : Type u_1} → (s : Finset α) → Fintype { x // x ∈ s }

Body:
fun {α} s => { elems := s.attach, complete := ⋯ }

## BASE-LIBRARY REF Finset.attach
{α : Type u_1} → (s : Finset α) → Finset { x // x ∈ s }

Body:
fun {α} s => { val := s.val.attach, nodup := ⋯ }

Docstring: `attach s` takes the elements of `s` and forms a new set of elements of the subtype
`{x // x ∈ s}`. 

## BASE-LIBRARY REF Finset.mem_attach
∀ {α : Type u_1} (s : Finset α) (x : { x // x ∈ s }), x ∈ s.attach

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Body:
fun {α} [Fintype α] => Fintype.elems

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## INFORMAL STATEMENT
lem.fps.infprod.claim11

\leanhelper  \textbf{(Claim 11.)} For a finite index set $I_n$, 

\[  \prod _{i \in I_n} \sum _{k \in S_i} p_{i,k} = \sum _{(k_i) \in S^{I_n}} \prod _{i \in I_n} p_{i,k_i}.  \]

 This is the standard finite distributive law (product of sums equals sum of products).

## VERDICT
{
  "verdict": "faithful",
  "discrepancies": [],
  "justification": "The formal equality exactly realizes the finite distributive law in the blueprint. The left side `\u220f i \u2208 In, \u2211 k \u2208 S i, p i k` matches `\u220f_{i \u2208 I_n} \u2211_{k \u2208 S_i} p_{i,k}`. On the right, `Fintype.piFinset fun i => S \u2191i` is the finite set of all functions on the subtype `{i // i \u2208 In}` selecting an element of each `S i`, so `\u2211 f \u2208 ...` matches the sum over `(k_i) \u2208 S^{I_n}`; the inner `\u220f i, p (\u2191i) (f i)` ranges over that finite subtype and matches `\u220f_{i \u2208 I_n} p_{i,k_i}`. The `[DecidableEq I]` binder is only an encoding requirement for finsets."
}