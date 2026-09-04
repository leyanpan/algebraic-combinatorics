## TARGET AlgebraicCombinatorics.QBinomialRec.qBinomialEval_eq_qBinomial (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommRing R] (n k : ℕ) (q : R),
  AlgebraicCombinatorics.QBinomialRec.qBinomialEval n k q = AlgebraicCombinatorics.QBinomialRec.qBinomial q n k

Docstring: The combinatorial definition agrees with the recursive definition.
This connects Definition def.pars.qbinom.qbinom with the recurrence-based `qBinomial`.

The proof shows that both definitions satisfy the same recurrence relation
(q-Pascal's identity) and boundary conditions. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.QBinomialRec.qBinomialEval (def)
{R : Type u_1} → [CommRing R] → ℕ → ℕ → R → R

Body:
fun {R} [CommRing R] n k a =>
  Polynomial.eval₂ (Int.castRingHom R) a (AlgebraicCombinatorics.QBinomialRec.qBinomialPolyDef n k)

Docstring: The q-binomial coefficient evaluated at a ring element.
(Definition def.pars.qbinom.qbinom (b))

`[n choose k]_a = ∑_{λ} a^|λ|`

where λ ranges over all partitions with largest part ≤ n-k and length ≤ k.

This is the result of substituting `a` for `q` in the polynomial `[n choose k]_q`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.QBinomialRec.qBinomial (def)
{R : Type u_1} → [CommRing R] → R → ℕ → ℕ → R

Body:
fun {R} [CommRing R] q x x_1 =>
  Nat.brecOn (motive := fun x => ℕ → R) x
    (fun x f x_2 =>
      (match (motive := (x : ℕ) → ℕ → Nat.below (motive := fun x => ℕ → R) x → R) x, x_2 with
        | x, 0 => fun x => 1
        | 0, n.succ => fun x => 0
        | n.succ, k.succ => fun x => x.1 k + q ^ (k + 1) * x.1 (k + 1))
        f)
    x_1

Docstring: The q-binomial coefficient (Gaussian binomial coefficient)
`[n choose k]_q = [n]_q! / ([k]_q! · [n-k]_q!)`.

This is defined as a polynomial in q with integer coefficients.
It counts partitions that fit in a k × (n-k) box, weighted by q^|λ|.

We use the recurrence relation (q-Pascal's identity):
[n choose k]_q = [n-1 choose k-1]_q + q^k · [n-1 choose k]_q

This avoids division and works over any commutative ring.

This definition is equivalent to `AlgebraicCombinatorics.qBinomial` in `QBinomialBasic.lean`,
which uses the monotone function sum definition. The equivalence is proven in
`qBinomial_eq_sum_monotone`. The argument order here is `(q : R) (n k : ℕ)` vs
`(n k : ℕ) (q : R)` in `QBinomialBasic.lean`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.QBinomialRec.qBinomialPolyDef (def)
ℕ → ℕ → Polynomial ℤ

Body:
fun n k =>
  if k ≤ n then
    ∑ size ∈ Finset.range (k * (n - k) + 1),
      AlgebraicCombinatorics.QBinomialRec.countPartitionsInBox size k (n - k) • Polynomial.X ^ size
  else 0

Docstring: The q-binomial coefficient as a polynomial in ℤ[q].
(Definition def.pars.qbinom.qbinom (a))

`[n choose k]_q = ∑_{λ} q^|λ|`

where λ ranges over all partitions with largest part ≤ n-k and length ≤ k.

This is a polynomial (not just a formal power series) because there are
finitely many such partitions - they all fit in a k × (n-k) box, so their
size is at most k · (n-k).

When k > n, this is 0 (the empty sum, since n - k < 0 means no partitions qualify). 

## PROJECT DEPENDENCY AlgebraicCombinatorics.QBinomialRec.countPartitionsInBox (def)
ℕ → ℕ → ℕ → ℕ

Body:
fun size k m => (AlgebraicCombinatorics.QBinomialRec.partitionsInBox size k m).card

Docstring: The count of partitions of a given size that fit in a k × m box. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.QBinomialRec.partitionsInBox (def)
(size : ℕ) → ℕ → ℕ → Finset size.Partition

Body:
fun size k m =>
  {p |
    AlgebraicCombinatorics.QBinomialRec.partitionLengthLeq p k ∧
      AlgebraicCombinatorics.QBinomialRec.partitionLargestPartLeq p m}

Docstring: The set of partitions of a given size that fit in a k × m box
(i.e., have length ≤ k and largest part ≤ m).

For the q-binomial `[n choose k]_q`, we use m = n - k.

**Argument order:** `(size k m : ℕ)` where:
- `size` is the partition size
- `k` is the maximum number of parts (length ≤ k)
- `m` is the maximum part size (largest part ≤ m)

This matches the convention in `AlgebraicCombinatorics.partitionsInBox` from `QBinomialBasic.lean`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.QBinomialRec.partitionLengthLeq (def)
{n : ℕ} → n.Partition → ℕ → Prop

Body:
fun {n} p k => p.parts.card ≤ k

Docstring: A partition has length ≤ k if it has at most k parts.
This is used in the combinatorial definition of q-binomial coefficients. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.QBinomialRec.partitionLargestPartLeq (def)
{n : ℕ} → n.Partition → ℕ → Prop

Body:
fun {n} p m => ∀ i ∈ p.parts, i ≤ m

Docstring: A partition has largest part ≤ m if all parts are ≤ m.
This is used in the combinatorial definition of q-binomial coefficients. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.QBinomialRec.instDecidablePartitionLengthLeq (def)
{n k : ℕ} → (p : n.Partition) → Decidable (AlgebraicCombinatorics.QBinomialRec.partitionLengthLeq p k)

Body:
fun {n k} p => inferInstanceAs (Decidable (p.parts.card ≤ k))

## PROJECT DEPENDENCY AlgebraicCombinatorics.QBinomialRec.instDecidablePartitionLargestPartLeq (def)
{n m : ℕ} → (p : n.Partition) → Decidable (AlgebraicCombinatorics.QBinomialRec.partitionLargestPartLeq p m)

Body:
fun {n m} p => inferInstanceAs (Decidable (∀ i ∈ p.parts, i ≤ m))

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Polynomial.eval₂
{R : Type u_1} → {S : Type u_2} → [inst : Semiring R] → [inst_1 : Semiring S] → (R →+* S) → S → Polynomial R → S

Body:
Polynomial.wrapped✝.1

Docstring: Evaluate a polynomial `p` given a ring hom `f` from the scalar ring
to the target and a value `x` for the variable in the target 

## BASE-LIBRARY REF Int.instSemiring
Semiring ℤ

Body:
inferInstance

## BASE-LIBRARY REF Semiring
Type u → Type u

Docstring: A `Semiring` is a type with addition, multiplication, a `0` and a `1` where addition is
commutative and associative, multiplication is associative and left and right distributive over
addition, and `0` and `1` are additive and multiplicative identities. 

## BASE-LIBRARY REF Int.instCommSemiring
CommSemiring ℤ

Body:
inferInstance

## BASE-LIBRARY REF CommRing.mul_comm
∀ {α : Type u} [self : CommRing α] (a b : α), a * b = b * a

Docstring: Multiplication is commutative in a commutative multiplicative magma. 

## BASE-LIBRARY REF Int.castRingHom
(α : Type u_3) → [inst : NonAssocRing α] → ℤ →+* α

Body:
fun α [NonAssocRing α] => { toFun := Int.cast, map_one' := ⋯, map_mul' := ⋯, map_zero' := ⋯, map_add' := ⋯ }

Docstring: `coe : ℤ → α` as a `RingHom`. 

## BASE-LIBRARY REF NonAssocCommRing
Type u → Type u

Docstring: A non-associative commutative ring is a `NonAssocRing` with commutative multiplication. 

## BASE-LIBRARY REF CommRing.toNonAssocCommRing._proof_1
∀ {α : Type u_1} [inst : CommRing α] (a b : α), a * b = b * a

## BASE-LIBRARY REF Nat.brecOn
{motive : ℕ → Sort u} → (t : ℕ) → ((t : ℕ) → Nat.below t → motive t) → motive t

Body:
fun {motive} t F_1 => (Nat.brecOn.go t F_1).1

## BASE-LIBRARY REF Nat.below
{motive : ℕ → Sort u} → ℕ → Sort (max 1 u)

Body:
fun {motive} t => Nat.rec PUnit.{max 1 u} (fun n n_ih => motive n ×' n_ih) t

## BASE-LIBRARY REF Nat.brecOn.go
{motive : ℕ → Sort u} → (t : ℕ) → ((t : ℕ) → Nat.below t → motive t) → motive t ×' Nat.below t

Body:
fun {motive} t F_1 => Nat.rec ⟨F_1 Nat.zero PUnit.unit, PUnit.unit⟩ (fun n n_ih => ⟨F_1 n.succ n_ih, n_ih⟩) t

## BASE-LIBRARY REF One
Type u → Type u

Docstring: A type with a "one" element. 

## BASE-LIBRARY REF One.one
{α : Type u} → [self : One α] → α

Body:
fun α [self : One α] => self.1

Docstring: The "one" element of the type. 

## BASE-LIBRARY REF AddMonoidWithOne
Type u_2 → Type u_2

Docstring: An `AddMonoidWithOne` is an `AddMonoid` with a `1`.
It also contains data for the unique homomorphism `ℕ → R`. 

## BASE-LIBRARY REF AddGroupWithOne
Type u → Type u

Docstring: An `AddGroupWithOne` is an `AddGroup` with a 1. It also contains data for the unique
homomorphisms `ℕ → R` and `ℤ → R`. 

## BASE-LIBRARY REF Ring
Type u → Type u

Docstring: A `Ring` is a `Semiring` with negation making it an additive group. 

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

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing._proof_1
∀ {α : Type u_1} [s : CommRing α] (a b : α), a - b = a + -b

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing._proof_2
∀ {α : Type u_1} [s : CommRing α] (a : α), Ring.zsmul 0 a = 0

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing._proof_3
∀ {α : Type u_1} [s : CommRing α] (n : ℕ) (a : α), Ring.zsmul (↑n.succ) a = Ring.zsmul (↑n) a + a

## BASE-LIBRARY REF Nat.succ
ℕ → ℕ

Docstring: The successor of a natural number `n`.

Using `Nat.succ n` should usually be avoided in favor of `n + 1`, which is the [simp normal
form](https://lean-lang.org/doc/reference/4.28.0/find/?domain=Verso.Genre.Manual.section&name=simp-normal-forms).


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

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.left_distrib
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a b c : α), a * (b + c) = a * b + a * c

Docstring: Multiplication is left distributive over addition 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.right_distrib
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a b c : α), (a + b) * c = a * c + b * c

Docstring: Multiplication is right distributive over addition 

## BASE-LIBRARY REF Mul
Type u → Type u

Docstring: The homogeneous version of `HMul`: `a * b : α` where `a b : α`. 

## BASE-LIBRARY REF Mul.mul
{α : Type u} → [self : Mul α] → α → α → α

Body:
fun α [self : Mul α] => self.1

Docstring: `a * b` computes the product of `a` and `b`. See `HMul`. 

## BASE-LIBRARY REF Pow
Type u → Type v → Type (max u v)

Docstring: The homogeneous version of `HPow`: `a ^ b : α` where `a : α`, `b : β`.
(The right argument is not the same as the left since we often want this even
in the homogeneous case.)

Types can choose to subscribe to particular defaulting behavior by providing
an instance to either `NatPow` or `HomogeneousPow`:
- `NatPow` is for types whose exponents is preferentially a `Nat`.
- `HomogeneousPow` is for types whose base and exponent are preferentially the same.


## BASE-LIBRARY REF Pow.pow
{α : Type u} → {β : Type v} → [self : Pow α β] → α → β → α

Body:
fun α β [self : Pow α β] => self.1

Docstring: `a ^ b` computes `a` to the power of `b`. See `HPow`. 

## BASE-LIBRARY REF Monoid
Type u → Type u

Docstring: A `Monoid` is a `Semigroup` with an element `1` such that `1 * a = a * 1 = a`. 

## BASE-LIBRARY REF MonoidWithZero
Type u → Type u

Docstring: A type `M₀` is a “monoid with zero” if it is a monoid with zero element, and `0` is left
and right absorbing. 

## BASE-LIBRARY REF NonUnitalSemiring.mul_assoc
∀ {α : Type u} [self : NonUnitalSemiring α] (a b c : α), a * b * c = a * (b * c)

Docstring: Multiplication is associative 

## BASE-LIBRARY REF Semiring.one_mul
∀ {α : Type u} [self : Semiring α] (a : α), 1 * a = a

Docstring: One is a left neutral element for multiplication 

## BASE-LIBRARY REF Semiring.mul_one
∀ {α : Type u} [self : Semiring α] (a : α), a * 1 = a

Docstring: One is a right neutral element for multiplication 

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


## BASE-LIBRARY REF Polynomial
(R : Type u_1) → [Semiring R] → Type u_1

Docstring: `Polynomial R` is the type of univariate polynomials over `R`,
denoted as `R[X]` within the `Polynomial` namespace.

Polynomials should be seen as (semi-)rings with the additional constructor `X`.
The embedding from `R` is called `C`. 

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


## BASE-LIBRARY REF Nat.le
ℕ → ℕ → Prop

Docstring: Non-strict, or weak, inequality of natural numbers, usually accessed via the `≤` operator.


## BASE-LIBRARY REF Nat.decLe
(n m : ℕ) → Decidable (n ≤ m)

Body:
fun n m => if h : n.ble m = true then isTrue ⋯ else isFalse ⋯

Docstring: A decision procedure for non-strict inequality of natural numbers, usually accessed via the
`DecidableLE Nat` instance.

Examples:
 * `(if 3 ≤ 4 then "yes" else "no") = "yes"`
 * `(if 6 ≤ 4 then "yes" else "no") = "no"`
 * `show 12 ≤ 12 by decide`
 * `show 5 ≤ 12 by decide`


## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Body:
fun {ι} {M} [AddCommMonoid M] s f => (Multiset.map f s.val).sum

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Polynomial.commRing
{R : Type u} → [inst : CommRing R] → CommRing (Polynomial R)

Body:
fun {R} [CommRing R] =>
  let __Ring := Polynomial.ring;
  { toRing := __Ring, mul_comm := ⋯ }

## BASE-LIBRARY REF Polynomial.ring
{R : Type u} → [inst : Ring R] → Ring (Polynomial R)

Body:
fun {R} [Ring R] =>
  { toSemiring := Polynomial.semiring, toNeg := Polynomial.instNeg, toSub := Polynomial.instSub, sub_eq_add_neg := ⋯,
    zsmul := fun n x => n • x, zsmul_zero' := ⋯, zsmul_succ' := ⋯, zsmul_neg' := ⋯, neg_add_cancel := ⋯,
    toIntCast := Polynomial.instIntCast, intCast_ofNat := ⋯, intCast_negSucc := ⋯ }

## BASE-LIBRARY REF Polynomial.commRing._proof_1
∀ {R : Type u_1} [inst : CommRing R] (a b : Polynomial R), a * b = b * a

## BASE-LIBRARY REF Int.instCommRing
CommRing ℤ

Body:
let __spread.0 := Int.instAddCommGroup;
let __spread.1 := Int.instCommSemigroup;
{ toAddMonoid := __spread.0.toAddMonoid, add_comm := ⋯, toMul := __spread.1.toMul, left_distrib := Int.mul_add,
  right_distrib := Int.add_mul, zero_mul := Int.zero_mul, mul_zero := Int.mul_zero,
  mul_assoc := Int.instCommRing._proof_3, toOne := Int.instMonoid.toMulOneClass.toOne, one_mul := Int.one_mul,
  mul_one := Int.mul_one, natCast := fun x => ↑x, natCast_zero := Int.instCommRing._proof_4,
  natCast_succ := Int.instCommRing._proof_5, npow := fun n x => x ^ n, npow_zero := ⋯, npow_succ := ⋯,
  toNeg := __spr …

## BASE-LIBRARY REF AddCommGroup
Type u → Type u

Docstring: An additive commutative group is an additive group with commutative `(+)`. 

## BASE-LIBRARY REF Int.instAddCommGroup
AddCommGroup ℤ

Body:
{ toAdd := Int.instAdd, add_assoc := Int.add_assoc, toZero := Zero.ofOfNat0, zero_add := Int.zero_add,
  add_zero := Int.add_zero, nsmul := fun x1 x2 => ↑x1 * x2, nsmul_zero := Int.zero_mul,
  nsmul_succ := Int.instAddCommGroup._proof_1, toNeg := Int.instNegInt, toSub := Int.instSub, sub_eq_add_neg := ⋯,
  zsmul := fun x1 x2 => x1 * x2, zsmul_zero' := Int.zero_mul, zsmul_succ' := ⋯, zsmul_neg' := ⋯,
  neg_add_cancel := Int.add_left_neg, add_comm := Int.add_comm }

## BASE-LIBRARY REF CommSemigroup
Type u → Type u

Docstring: A commutative semigroup is a type with an associative commutative `(*)`. 

## BASE-LIBRARY REF Int.instCommSemigroup
CommSemigroup ℤ

Body:
inferInstance

## BASE-LIBRARY REF Int.mul_add
∀ (a b c : ℤ), a * (b + c) = a * b + a * c

## BASE-LIBRARY REF Int.add_mul
∀ (a b c : ℤ), (a + b) * c = a * c + b * c

## BASE-LIBRARY REF Int.zero_mul
∀ (a : ℤ), 0 * a = 0

## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Body:
fun n => { val := Multiset.range n, nodup := ⋯ }

Docstring: `range n` is the set of natural numbers less than `n`. 

## BASE-LIBRARY REF Nat.mul
ℕ → ℕ → ℕ

Body:
fun x x_1 =>
  Nat.brecOn (motive := fun x => ℕ → ℕ) x_1
    (fun x f x_2 =>
      (match (motive := ℕ → (x : ℕ) → Nat.below (motive := fun x => ℕ → ℕ) x → ℕ) x_2, x with
        | x, 0 => fun x => 0
        | a, b.succ => fun x => (x.1 a).add a)
        f)
    x

Docstring: Multiplication of natural numbers, usually accessed via the `*` operator.

This function is overridden in both the kernel and the compiler to efficiently evaluate using the
arbitrary-precision arithmetic library. The definition provided here is the logical model.


## BASE-LIBRARY REF Sub
Type u → Type u

Docstring: The homogeneous version of `HSub`: `a - b : α` where `a b : α`. 

## BASE-LIBRARY REF Sub.sub
{α : Type u} → [self : Sub α] → α → α → α

Body:
fun α [self : Sub α] => self.1

Docstring: `a - b` computes the difference of `a` and `b`. See `HSub`. 

## BASE-LIBRARY REF instSubNat
Sub ℕ

Body:
{ sub := Nat.sub }

Characterization: Natural subtraction truncates: `a - b = 0` whenever `b ≥ a`.

## BASE-LIBRARY REF Nat.sub
ℕ → ℕ → ℕ

Body:
fun x x_1 =>
  Nat.brecOn (motive := fun x => ℕ → ℕ) x_1
    (fun x f x_2 =>
      (match (motive := ℕ → (x : ℕ) → Nat.below (motive := fun x => ℕ → ℕ) x → ℕ) x_2, x with
        | a, 0 => fun x => a
        | a, b.succ => fun x => (x.1 a).pred)
        f)
    x

Docstring: Subtraction of natural numbers, truncated at `0`. Usually used via the `-` operator.

If a result would be less than zero, then the result is zero.

This definition is overridden in both the kernel and the compiler to efficiently evaluate using the
arbitrary-precision arithmetic library. The definition provided here is the logical model.

Examples:
* `5 - 3 = 2`
* `8 - 2 = 6`
* `8 - 8 = 0`
* `8 - 20 = 0`


Characterization: Natural subtraction truncates: `a - b = 0` whenever `b ≥ a`.

## BASE-LIBRARY REF SMul
Type u → Type v → Type (max u v)

Docstring: Typeclass for types with a scalar multiplication operation, denoted `•` (`\bu`) 

## BASE-LIBRARY REF SMul.smul
{M : Type u} → {α : Type v} → [self : SMul M α] → M → α → α

Body:
fun M α [self : SMul M α] => self.1

Docstring: `m • a : α` denotes the product of `m : M` and `a : α`. The meaning of this notation is type-dependent,
but it is intended to be used for left actions. 

## BASE-LIBRARY REF Polynomial.instNSMul
{R : Type u} → [inst : Semiring R] → SMul ℕ (Polynomial R)

Body:
fun {R} [Semiring R] => { smul := fun r p => { toFinsupp := r • p.toFinsupp } }

## BASE-LIBRARY REF Polynomial.ofFinsupp
{R : Type u_1} → [inst : Semiring R] → AddMonoidAlgebra R ℕ → Polynomial R

## BASE-LIBRARY REF AddMonoidAlgebra
(R : Type u_8) → Type u_9 → [Semiring R] → Type (max u_8 u_9)

Body:
fun R M [Semiring R] => M →₀ R

Docstring: The additive monoid algebra over a semiring `R` generated by the additive monoid `M`.

It is the type of finite formal `R`-linear combinations of terms of `M`,
endowed with the convolution product. 

## BASE-LIBRARY REF AddMonoidAlgebra.nonAssocSemiring
{R : Type u_1} → {M : Type u_4} → [inst : Semiring R] → [AddZeroClass M] → NonAssocSemiring (AddMonoidAlgebra R M)

Body:
fun {R} {M} [Semiring R] [AddZeroClass M] =>
  { toNonUnitalNonAssocSemiring := AddMonoidAlgebra.nonUnitalNonAssocSemiring, toOne := AddMonoidAlgebra.zero,
    one_mul := ⋯, mul_one := ⋯, natCast := fun n => AddMonoidAlgebra.single 0 ↑n, natCast_zero := ⋯, natCast_succ := ⋯ }

## BASE-LIBRARY REF Nat.instAddMonoid
AddMonoid ℕ

Body:
inferInstance

## BASE-LIBRARY REF Polynomial.semiring
{R : Type u} → [inst : Semiring R] → Semiring (Polynomial R)

Body:
fun {R} [Semiring R] =>
  { toAdd := Polynomial.instAdd, add_assoc := ⋯, toZero := Polynomial.instZero, zero_add := ⋯, add_zero := ⋯,
    nsmul := fun n x => n • x, nsmul_zero := ⋯, nsmul_succ := ⋯, add_comm := ⋯, toMul := Polynomial.instMul,
    left_distrib := ⋯, right_distrib := ⋯, zero_mul := ⋯, mul_zero := ⋯, mul_assoc := ⋯, toOne := Polynomial.instOne,
    one_mul := ⋯, mul_one := ⋯, toNatCast := Polynomial.instNatCast, natCast_zero := ⋯, natCast_succ := ⋯,
    npow := Monoid.npow, npow_zero := ⋯, npow_succ := ⋯ }

## BASE-LIBRARY REF Polynomial.instAdd
{R : Type u} → [inst : Semiring R] → Add (Polynomial R)

Body:
fun {R} [Semiring R] =>
  {
    add := fun x x_1 =>
      match x with
      | { toFinsupp := a } =>
        match x_1 with
        | { toFinsupp := b } => { toFinsupp := a + b } }

## BASE-LIBRARY REF Polynomial.semiring._proof_1
∀ {R : Type u_1} [inst : Semiring R] (a b c : Polynomial R), a + b + c = a + (b + c)

## BASE-LIBRARY REF Polynomial.instZero
{R : Type u} → [inst : Semiring R] → Zero (Polynomial R)

Body:
fun {R} [Semiring R] => { zero := { toFinsupp := 0 } }

## BASE-LIBRARY REF Polynomial.semiring._proof_2
∀ {R : Type u_1} [inst : Semiring R] (a : Polynomial R), 0 + a = a

## BASE-LIBRARY REF Polynomial.semiring._proof_3
∀ {R : Type u_1} [inst : Semiring R] (a : Polynomial R), a + 0 = a

## BASE-LIBRARY REF Polynomial.semiring._proof_4
∀ {R : Type u_1} [inst : Semiring R] (x : Polynomial R), 0 • x = 0

## BASE-LIBRARY REF Polynomial.semiring._proof_5
∀ {R : Type u_1} [inst : Semiring R] (n : ℕ) (x : Polynomial R), (n + 1) • x = n • x + x

## BASE-LIBRARY REF Polynomial.semiring._proof_6
∀ {R : Type u_1} [inst : Semiring R] (a b : Polynomial R), a + b = b + a

## BASE-LIBRARY REF Polynomial.instMul
{R : Type u} → [inst : Semiring R] → Mul (Polynomial R)

Body:
fun {R} [Semiring R] =>
  {
    mul := fun x x_1 =>
      match x with
      | { toFinsupp := a } =>
        match x_1 with
        | { toFinsupp := b } => { toFinsupp := a * b } }

## BASE-LIBRARY REF Polynomial.semiring._proof_7
∀ {R : Type u_1} [inst : Semiring R] (a b c : Polynomial R), a * (b + c) = a * b + a * c

## BASE-LIBRARY REF Polynomial.X
{R : Type u} → [inst : Semiring R] → Polynomial R

Body:
fun {R} [Semiring R] => (Polynomial.monomial 1) 1

Docstring: `X` is the polynomial variable (aka indeterminate). 

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Body:
fun {α} s => s.val.card

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Nat.Partition
ℕ → Type

Docstring: A partition of `n` is a multiset of positive integers summing to `n`. 

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Body:
fun {α} p [DecidablePred p] s => { val := Multiset.filter p s.val, nodup := ⋯ }

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF instDecidableAnd.match_1
{q : Prop} →
  (motive : Decidable q → Sort u_1) →
    (dq : Decidable q) → ((hq : q) → motive (isTrue hq)) → ((hq : ¬q) → motive (isFalse hq)) → motive dq

Body:
fun {q} motive dq h_1 h_2 => Decidable.casesOn dq (fun h => h_2 h) fun h => h_1 h

## BASE-LIBRARY REF Decidable.isTrue
{p : Prop} → p → Decidable p

Docstring: Proves that `p` is decidable by supplying a proof of `p` 

## BASE-LIBRARY REF And.intro
∀ {a b : Prop}, a → b → a ∧ b

Docstring: `And.intro : a → b → a ∧ b` is the constructor for the And operation. 

## BASE-LIBRARY REF Decidable.isFalse
{p : Prop} → ¬p → Decidable p

Docstring: Proves that `p` is decidable by supplying a proof of `¬p` 

## BASE-LIBRARY REF instDecidableAnd._proof_1
∀ {p q : Prop}, ¬q → p ∧ q → False

## BASE-LIBRARY REF instDecidableAnd._proof_2
∀ {p q : Prop}, ¬p → p ∧ q → False

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Body:
fun {α} [Fintype α] => Fintype.elems

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Nat.Partition.instFintype
(n : ℕ) → Fintype n.Partition

Body:
fun n => Fintype.ofSurjective (Nat.Partition.ofComposition n) ⋯

Docstring: Show there are finitely many partitions by considering the surjection from compositions to
partitions.


## BASE-LIBRARY REF Multiset.card
{α : Type u_1} → Multiset α → ℕ

Body:
fun {α} => Quot.lift List.length ⋯

Docstring: The cardinality of a multiset is the sum of the multiplicities
of all its elements, or simply the length of the underlying list. 

## BASE-LIBRARY REF Nat.Partition.parts
{n : ℕ} → n.Partition → Multiset ℕ

Body:
fun n self => self.1

Docstring: positive integers summing to `n` 

## BASE-LIBRARY REF Multiset
Type u → Type u

Body:
fun α => Quotient (List.isSetoid α)

Docstring: `Multiset α` is the quotient of `List α` by list permutation. The result
is a type of finite sets with duplicates allowed. 

## BASE-LIBRARY REF Multiset.Mem
{α : Type u_1} → Multiset α → α → Prop

Body:
fun {α} s a => Quot.liftOn s (fun l => a ∈ l) ⋯

Docstring: `a ∈ s` means that `a` has nonzero multiplicity in `s`. 

## BASE-LIBRARY REF inferInstanceAs
(α : Sort u) → [i : α] → α

Body:
fun α [i : α] => i

Docstring: `inferInstanceAs α` synthesizes a value of any target type by typeclass
inference. This is just like `inferInstance` except that `α` is given
explicitly instead of being inferred from the target type. It is especially
useful when the target type is some `α'` which is definitionally equal to `α`,
but the instance we are looking for is only registered for `α` (because
typeclass search does not unfold most definitions, but definitional equality
does.) Example:
```
#check inferInstanceAs (Inhabited Nat) -- Inhabited Nat
```


## BASE-LIBRARY REF Multiset.decidableDforallMultiset
{α : Type u_1} →
  {m : Multiset α} →
    {p : (a : α) → a ∈ m → Prop} →
      [_hp : (a : α) → (h : a ∈ m) → Decidable (p a h)] → Decidable (∀ (a : α) (h : a ∈ m), p a h)

Body:
fun {α} {m} {p} [(a : α) → (h : a ∈ m) → Decidable (p a h)] => decidable_of_iff (∀ a ∈ m.attach, p ↑a ⋯) ⋯

## BASE-LIBRARY REF decidable_of_iff
{b : Prop} → (a : Prop) → (a ↔ b) → [Decidable a] → Decidable b

Body:
fun {b} a h [Decidable a] => decidable_of_decidable_of_iff h

Docstring: Transfer decidability of `a` to decidability of `b`, if the propositions are equivalent.
**Important**: this function should be used instead of `rw` on `Decidable b`, because the
kernel will get stuck reducing the usage of `propext` otherwise,
and `decide` will not work. 

## BASE-LIBRARY REF Multiset.attach
{α : Type u_1} → (s : Multiset α) → Multiset { x // x ∈ s }

Body:
fun {α} s => Multiset.pmap Subtype.mk s ⋯

Docstring: "Attach" a proof that `a ∈ s` to each element `a` in `s` to produce
a multiset on `{x // x ∈ s}`. 

## BASE-LIBRARY REF Multiset.decidableDforallMultiset._proof_1
∀ {α : Type u_1} {m : Multiset α} (a : { x // x ∈ m }), ↑a ∈ m

## BASE-LIBRARY REF Multiset.decidableDforallMultiset._proof_2
∀ {α : Type u_1} {m : Multiset α} {p : (a : α) → a ∈ m → Prop}, (∀ a ∈ m.attach, p ↑a ⋯) ↔ ∀ (a : α) (h : a ∈ m), p a h

## BASE-LIBRARY REF Multiset.decidableForallMultiset
{α : Type u_1} → {m : Multiset α} → {p : α → Prop} → [(a : α) → Decidable (p a)] → Decidable (∀ a ∈ m, p a)

Body:
fun {α} {m} {p} [(a : α) → Decidable (p a)] => Quotient.recOnSubsingleton m fun l => decidable_of_iff (∀ a ∈ l, p a) ⋯

Docstring: If `p` is a decidable predicate,
so is the predicate that all elements of a multiset satisfy `p`. 

## INFORMAL STATEMENT
thm.qbinomial-formulas.eval-eq-qbinomial

\leanhelper  The combinatorial definition (sum over partitions) agrees with the recurrence-based definition from Definition~ \ref{def.pars.qbinom.qbinom}: for all $n, k \in \mathbb {N}$ and ring element $q$, 

\[  \mathrm{qBinomialEval}(n, k, q) = \binom {n}{k}_q.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.comps
def.fps.comps

\textbf{(a)} An \emph{(integer) composition} means a (finite) tuple of positive integers. \medskip 

\textbf{(b)} The \emph{size} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $\alpha _{1}+\alpha _{2}+\cdots +\alpha _{m}$. It is written $\left\vert \alpha \right\vert $. \medskip 

\textbf{(c)} The \emph{length} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $m$. It is written $\ell \left( \alpha \right) $. \medskip 

\textbf{(d)} Let $n\in \mathbb {N}$. A \emph{composition of }$n$ means a composition whose size is $n$. \medskip 

\textbf{(e)} Let $n\in \mathbb {N}$ and $k\in \mathbb {N}$. A \emph{composition of }$n$\emph{ into }$k$\emph{ parts} is a composition whose size is $n$ and whose length is $k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pars.parts
def.pars.parts

\textbf{(a)} An \emph{(integer) partition} means a (finite) weakly decreasing tuple of positive integers – i.e., a finite tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{m}\right) $ of positive integers such that $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{m}$. 

Thus, partitions are the same as weakly decreasing compositions. Hence, the notions of \emph{size} and \emph{length} of a partition are automatically defined, since we have defined them for compositions (in Definition \ref{def.fps.comps}). \medskip 

\textbf{(b)} The \emph{parts} of a partition $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{m}\right) $ are simply its entries $\lambda _{1},\lambda _{2},\ldots ,\lambda _{m}$. \medskip 

\textbf{(c)} Let $n\in \mathbb {Z}$. A \emph{partition of }$n$ means a partition whose size is $n$. \medskip 

\textbf{(d)} Let $n\in \mathbb {Z}$ and $k\in \mathbb {N}$. A \emph{partition of }$n$\emph{ into }$k$\emph{ parts} is a partition whose size is $n$ and whose length is $k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pars.qbinom.qbinom
def.pars.qbinom.qbinom

Let $n\in \mathbb {N}$ and $k\in \mathbb {Z}$. 

\textbf{(a)} The $q$-binomial coefficient (or Gaussian binomial coefficient) $\binom {n}{k}_{q}$ is defined to be the polynomial 

\[  \sum _{\substack {\lambda \text{ is a partition}\\ \text{with largest part }\leq n-k\\ \text{and length }\leq k}}q^{|\lambda |}\in \mathbb {Z}[q].  \]

\textbf{(b)} If $a$ is any element of a ring $A$, then we set 

\[  \binom {n}{k}_{a} := \binom {n}{k}_{q}[a] = \sum _{\substack {\lambda \text{ is a partition}\\ \text{with largest part }\leq n-k\\ \text{and length }\leq k}}a^{|\lambda |}\in A.  \]

## VERDICT
{
  "verdict": "minor_discrepancy",
  "discrepancies": [
    {
      "root": "[inst : CommRing R]",
      "severity": "minor",
      "bridge": "For an arbitrary ring A and q : A, first apply the formal theorem universally in the commutative polynomial ring \u2124[X] (with q = X), obtaining the corresponding polynomial identity. Evaluating that identity at q in A recovers the claimed equality. Integer coefficients commute with every element of a unital ring, and a routine induction shows that evaluation also transports the recurrence-based expression. Thus noncommutative rings are recoverable by a standard universal-polynomial reduction, without repeating the combinatorial proof."
    }
  ],
  "justification": "The blueprint says \u201cIf a is any element of a ring A\u201d and the theorem states the equality for a \u201cring element q,\u201d whereas the elaborated signature quantifies only `\u2200 {R : Type u_1} [inst : CommRing R] ...`. Hence the formal theorem cannot be instantiated directly for a noncommutative ring. Apart from that restriction, unfolding `qBinomialEval` and `qBinomialPolyDef` gives the stated sum over partitions (with the explicit zero case when `k > n`), while unfolding `qBinomial` gives the recurrence-based Gaussian coefficient, so the asserted equality matches the blueprint."
}