## TARGET AlgebraicCombinatorics.SignedCounting.blocky_sum_eq (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : Field K] {ω : K} {d : ℕ},
  IsPrimitiveRoot ω d →
    0 < d →
      ∀ (n k : ℕ),
        ∑ S ∈ AlgebraicCombinatorics.SignedCounting.blockySubsets d n k, ω ^ (S.sum id - (Finset.range k).sum id) =
          ↑((n / d).choose (k / d)) *
            (Polynomial.aeval ω) (AlgebraicCombinatorics.SignedCounting.qBinomial (n % d) (k % d))

Docstring: The sum of contributions from blocky subsets gives the product formula.

For blocky subsets, the contribution factors because:
1. Complete blocks contribute d*d*i + d*(d-1)/2 each, and since ω^d = 1,
   the ω^{d*d*i} part is always 1.
2. The partial block contributes independently.
3. The bijection with (block indices, partial elements) pairs allows factoring. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SignedCounting.blockySubsets (def)
ℕ → ℕ → ℕ → Finset (Finset ℕ)

Body:
fun d n k =>
  {S ∈ AlgebraicCombinatorics.SignedCounting.kSubsets n k | AlgebraicCombinatorics.SignedCounting.IsDBlocky d n S}

Docstring: The set of d-blocky k-element subsets of [n]. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SignedCounting.qBinomial (def)
ℕ → ℕ → Polynomial ℤ

Body:
fun n k => ∑ S ∈ (Finset.range n).powerset with S.card = k, Polynomial.X ^ (S.sum id - (Finset.range k).sum id)

Docstring: The q-binomial coefficient `[n choose k]_q = [n]_q! / ([k]_q! * [n-k]_q!)`.
This is well-defined as a polynomial (the division is exact).

We define it combinatorially using the sum over k-element subsets formula:
`[n choose k]_q = ∑_{S ⊆ [n], |S|=k} q^{sum(S) - (1+2+...+k)}`

**Note:** This is a local definition as `Polynomial ℤ`, equivalent to
`AlgebraicCombinatorics.qBinomial n k X` from `QBinomialBasic.lean` when the latter
is evaluated as a polynomial. The equivalence follows from `qBinomial_eq_sum_subsets`.
This definition uses 0-indexed sets `{0, 1, ..., n-1}` while `QBinomialBasic` uses
1-indexed sets `{1, 2, ..., n}` in its subset formula, but both are equivalent. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SignedCounting.IsDBlocky (def)
ℕ → ℕ → Finset ℕ → Prop

Body:
fun d n S => S ⊆ Finset.range n ∧ ∀ i < n / d, (∀ j < d, i * d + j ∈ S) ∨ ∀ j < d, i * d + j ∉ S

Docstring: A subset S of [n] is d-blocky if for each complete d-block {id, id+1, ..., id+d-1}
contained in [n], the set S either contains all elements or none of the elements. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SignedCounting.decidableIsDBlocky (def)
(d n : ℕ) → (S : Finset ℕ) → Decidable (AlgebraicCombinatorics.SignedCounting.IsDBlocky d n S)

Body:
fun d n S => id inferInstance

## PROJECT DEPENDENCY AlgebraicCombinatorics.SignedCounting.kSubsets (def)
ℕ → ℕ → Finset (Finset ℕ)

Body:
fun n k => Finset.powersetCard k (Finset.range n)

Docstring: The set of k-element subsets of [n]. 

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


## BASE-LIBRARY REF IsPrimitiveRoot
{M : Type u_1} → [CommMonoid M] → M → ℕ → Prop

Docstring: An element `ζ` is a primitive `k`-th root of unity if `ζ ^ k = 1`,
and if `l` satisfies `ζ ^ l = 1` then `k ∣ l`. 

## BASE-LIBRARY REF CommRing.toCommMonoid
{α : Type u} → [self : CommRing α] → CommMonoid α

## BASE-LIBRARY REF EuclideanDomain.toCommRing
{R : Type u} → [self : EuclideanDomain R] → CommRing R

## BASE-LIBRARY REF Field.toEuclideanDomain
{K : Type u_1} → [Field K] → EuclideanDomain K

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

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

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toAddCommMonoid
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → AddCommMonoid α

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

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

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF id
{α : Sort u} → α → α

Docstring: The identity function. `id` takes an implicit argument `α : Sort u`
(a type in any universe), and an argument `a : α`, and returns `a`.

Although this may look like a useless function, one application of the identity
function is to explicitly put a type on an expression. If `e` has type `T`,
and `T'` is definitionally equal to `T`, then `@id T' e` typechecks, and Lean
knows that this expression has type `T'` rather than `T`. This can make a
difference for typeclass inference, since `T` and `T'` may have different
typeclass instances on them. `show T' from e` is sugar for an `@id T' e`
expression.


## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Docstring: `range n` is the set of natural numbers less than `n`. 

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

## BASE-LIBRARY REF Nat.cast
{R : Type u} → [NatCast R] → ℕ → R

Docstring: The canonical homomorphism `Nat → R`. In most use cases, the target type will have a (semi)ring
structure, and this homomorphism should be a (semi)ring homomorphism.

`NatCast` and `IntCast` exist to allow different libraries with their own types that can be notated
as natural numbers to have consistent `simp` normal forms without needing to create coercion
simplification sets that are aware of all combinations. Libraries should make it easy to work with
`NatCast` where possible. For instance, in Mathlib there will be such a homomorphism (and thus a
`NatCast R` instance) whenever `R` is an additive monoid with a `1`.

The prototypical example is `Int.ofNat`.


## BASE-LIBRARY REF AddMonoidWithOne.toNatCast
{R : Type u_2} → [self : AddMonoidWithOne R] → NatCast R

## BASE-LIBRARY REF AddGroupWithOne.toAddMonoidWithOne
{R : Type u} → [self : AddGroupWithOne R] → AddMonoidWithOne R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF DivisionRing.toRing
{K : Type u_2} → [self : DivisionRing K] → Ring K

## BASE-LIBRARY REF Field.toDivisionRing
{K : Type u} → [self : Field K] → DivisionRing K

## BASE-LIBRARY REF Nat.choose
ℕ → ℕ → ℕ

Docstring: `choose n k` is the number of `k`-element subsets in an `n`-element set. Also known as binomial
coefficients. For the fact that this is the number of `k`-element-subsets of an `n`-element
set, see `Finset.card_powersetCard`. 

## BASE-LIBRARY REF HDiv.hDiv
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HDiv α β γ] → α → β → γ

Docstring: `a / b` computes the result of dividing `a` by `b`.
The meaning of this notation is type-dependent.
* For most types like `Nat`, `Int`, `Rat`, `Real`, `a / 0` is defined to be `0`.
* For `Nat`, `a / b` rounds downwards.
* For `Int`, `a / b` rounds downwards if `b` is positive or upwards if `b` is negative.
  It is implemented as `Int.ediv`, the unique function satisfying
  `a % b + b * (a / b) = a` and `0 ≤ a % b < natAbs b` for `b ≠ 0`.
  Other rounding conventions are available using the functions
  `Int.fdiv` (floor rounding) and `Int.tdiv` (truncation rounding).
* For `Float`, `a / 0` follows the IEEE 754 semantics for division,
  usually resulting in `inf` or `nan`. 

Conventions for notations in identifiers:

 * The recommended spelling of `/` in identifiers is `div`.

## BASE-LIBRARY REF instHDiv
{α : Type u_1} → [Div α] → HDiv α α α

## BASE-LIBRARY REF Nat.instDiv
Div ℕ

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF AlgHom
(R : Type u) →
  (A : Type v) →
    (B : Type w) →
      [inst : CommSemiring R] →
        [inst_1 : Semiring A] → [inst_2 : Semiring B] → [Algebra R A] → [Algebra R B] → Type (max v w)

Docstring: Defining the homomorphism in the category R-Alg, denoted `A →ₐ[R] B`. 

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Polynomial
(R : Type u_1) → [Semiring R] → Type u_1

Docstring: `Polynomial R` is the type of univariate polynomials over `R`,
denoted as `R[X]` within the `Polynomial` namespace.

Polynomials should be seen as (semi-)rings with the additional constructor `X`.
The embedding from `R` is called `C`. 

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF Int.instCommSemiring
CommSemiring ℤ

## BASE-LIBRARY REF Polynomial.semiring
{R : Type u} → [inst : Semiring R] → Semiring (Polynomial R)

## BASE-LIBRARY REF Polynomial.algebraOfAlgebra
{R : Type u} → {A : Type z} → [inst : CommSemiring R] → [inst_1 : Semiring A] → [Algebra R A] → Algebra R (Polynomial A)

Docstring: Note that this instance also provides `Algebra R R[X]`. 

## BASE-LIBRARY REF Algebra.id
(R : Type u) → [inst : CommSemiring R] → Algebra R R

Docstring: The identity map inducing an `Algebra` structure. 

## BASE-LIBRARY REF Ring.toIntAlgebra
(R : Type u_1) → [inst : Ring R] → Algebra ℤ R

Docstring: Ring ⥤ ℤ-Alg 

## BASE-LIBRARY REF AlgHom.funLike
{R : Type u} →
  {A : Type v} →
    {B : Type w} →
      [inst : CommSemiring R] →
        [inst_1 : Semiring A] →
          [inst_2 : Semiring B] → [inst_3 : Algebra R A] → [inst_4 : Algebra R B] → FunLike (A →ₐ[R] B) A B

## BASE-LIBRARY REF Polynomial.aeval
{R : Type u} →
  {A : Type z} → [inst : CommSemiring R] → [inst_1 : Semiring A] → [inst_2 : Algebra R A] → A → Polynomial R →ₐ[R] A

Docstring: Given a valuation `x` of the variable in an `R`-algebra `A`, `aeval R A x` is
the unique `R`-algebra homomorphism from `R[X]` to `A` sending `X` to `x`.

This is a stronger variant of the linear map `Polynomial.leval`. 

## BASE-LIBRARY REF HMod.hMod
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMod α β γ] → α → β → γ

Docstring: `a % b` computes the remainder upon dividing `a` by `b`.
The meaning of this notation is type-dependent.
* For `Nat` and `Int` it satisfies `a % b + b * (a / b) = a`,
  and `a % 0` is defined to be `a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `%` in identifiers is `mod`.

## BASE-LIBRARY REF instHMod
{α : Type u_1} → [Mod α] → HMod α α α

## BASE-LIBRARY REF Nat.instMod
Mod ℕ

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF Int.instSemiring
Semiring ℤ

## BASE-LIBRARY REF Polynomial.commRing
{R : Type u} → [inst : CommRing R] → CommRing (Polynomial R)

## BASE-LIBRARY REF Int.instCommRing
CommRing ℤ

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF Finset.powerset
{α : Type u_1} → Finset α → Finset (Finset α)

Docstring: When `s` is a finset, `s.powerset` is the finset of all subsets of `s` (seen as finsets). 

## BASE-LIBRARY REF Polynomial.X
{R : Type u} → [inst : Semiring R] → Polynomial R

Docstring: `X` is the polynomial variable (aka indeterminate). 

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF HasSubset.Subset
{α : Type u} → [self : HasSubset α] → α → α → Prop

Docstring: Subset relation: `a ⊆ b`  

Conventions for notations in identifiers:

 * The recommended spelling of `⊆` in identifiers is `subset`.

## BASE-LIBRARY REF Finset.instHasSubset
{α : Type u_1} → HasSubset (Finset α)

## BASE-LIBRARY REF Or
Prop → Prop → Prop

Docstring: `Or a b`, or `a ∨ b`, is the disjunction of propositions. There are two
constructors for `Or`, called `Or.inl : a → a ∨ b` and `Or.inr : b → a ∨ b`,
and you can use `match` or `cases` to destruct an `Or` assumption into the
two cases.


Conventions for notations in identifiers:

 * The recommended spelling of `∨` in identifiers is `or`.

 * The recommended spelling of `\/` in identifiers is `or` (prefer `∨` over `\/`).

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Finset.instMembership
{α : Type u_1} → Membership α (Finset α)

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

## BASE-LIBRARY REF instMulNat
Mul ℕ

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF Decidable
Prop → Type

Docstring: Either a proof that `p` is true or a proof that `p` is false. This is equivalent to a `Bool` paired
with a proof that the `Bool` is `true` if and only if `p` is true.

`Decidable` instances are primarily used via `if`-expressions and the tactic `decide`. In
conditional expressions, the `Decidable` instance for the proposition is used to select a branch. At
run time, this case distinction code is identical to that which would be generated for a
`Bool`-based conditional. In proofs, the tactic `decide` synthesizes an instance of `Decidable p`,
attempts to reduce it to `isTrue h`, and then succeeds with the proof `h` if it can.

Because `Decidable` carries data, when writing `@[simp]` lemmas which include a `Decidable` instance
on the LHS, it is best to use `{_ : Decidable p}` rather than `[Decidable p]` so that non-canonical
instances can be found via unification rather than instance synthesis.


## BASE-LIBRARY REF inferInstance
{α : Sort u} → [i : α] → α

Docstring: `inferInstance` synthesizes a value of any target type by typeclass
inference. This function has the same type signature as the identity
function, but the square brackets on the `[i : α]` argument means that it will
attempt to construct this argument by typeclass inference. (This will fail if
`α` is not a `class`.) Example:
```
#check (inferInstance : Inhabited Nat) -- Inhabited Nat

def foo : Inhabited (Nat × Nat) :=
  inferInstance

example : foo.default = (default, default) :=
  rfl
```


## BASE-LIBRARY REF instDecidableAnd
{p q : Prop} → [dp : Decidable p] → [dq : Decidable q] → Decidable (p ∧ q)

## BASE-LIBRARY REF Finset.instDecidableRelSubset
{α : Type u_1} → [DecidableEq α] → DecidableRel fun x1 x2 => x1 ⊆ x2

## BASE-LIBRARY REF Nat.decidableBallLT
(n : ℕ) →
  (P : (k : ℕ) → k < n → Prop) →
    [(n_1 : ℕ) → (h : n_1 < n) → Decidable (P n_1 h)] → Decidable (∀ (n_1 : ℕ) (h : n_1 < n), P n_1 h)

## BASE-LIBRARY REF instDecidableOr
{p q : Prop} → [dp : Decidable p] → [dq : Decidable q] → Decidable (p ∨ q)

## BASE-LIBRARY REF Finset.decidableMem
{α : Type u_1} → [_h : DecidableEq α] → (a : α) → (s : Finset α) → Decidable (a ∈ s)

## BASE-LIBRARY REF instDecidableNot
{p : Prop} → [dp : Decidable p] → Decidable ¬p

## BASE-LIBRARY REF Finset.powersetCard
{α : Type u_1} → ℕ → Finset α → Finset (Finset α)

Docstring: Given an integer `n` and a finset `s`, then `powersetCard n s` is the finset of subsets of `s`
of cardinality `n`. 

## INFORMAL STATEMENT
lem.blocky_sum_eq

\leanhelper  Let $K$ be a field, $d$ a positive integer, and $\omega $ a primitive $d$-th root of unity. For $n, k \in \mathbb {N}$, 

\[  \sum _{\substack {S \subseteq [n],\;  |S| = k,\\ S \text{ is $d$-blocky}}} \omega ^{\operatorname {sum}(S) - (0 + 1 + \cdots + (k-1))} = \binom {n/d}{k/d} \cdot \binom {n \bmod d}{k \bmod d}_{\omega }.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.det.k
conv.det.K

For the rest of this section, we fix a commutative ring $K$. In most examples, $K$ will be $\mathbb {Z}$ or $\mathbb {Q}$ or a polynomial ring.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.det.sum-compl
conv.det.sum-compl

For any subset $I$ of $[n]$, we write $\widetilde{I} = [n] \setminus I$ for its complement, and $\operatorname {sum} S = \sum _{s \in S} s$ for any finite set $S$ of integers.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.pars.qbinom.q
conv.pars.qbinom.q

In this section, we will mostly be using FPSs in the indeterminate $q$. That is, we call the indeterminate $q$ rather than $x$. The ring of FPSs in the indeterminate $q$ over a commutative ring $K$ will be denoted by $K[[q]]$. The ring of polynomials in the indeterminate $q$ over $K$ will be denoted by $K[q]$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.binom.binom
def.binom.binom

For any numbers $n$ and $k$, we set

\begin{equation}  \binom {n}{k}=\begin{cases}  \frac{n\left( n-1\right) \left( n-2\right) \cdots \left( n-k+1\right) }{k!}, &  \text{if }k\in \mathbb {N};\\ 0, &  \text{else.}\end{cases} \end{equation}

 Note that “numbers” is to be understood fairly liberally here. In particular, $n$ can be any integer, rational, real or complex number (or, more generally, any element in a $\mathbb {Q}$-algebra), whereas $k$ can be anything (although the only nonzero values of $\binom {n}{k}$ will be achieved for $k\in \mathbb {N}$, by the above definition).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.finsetsumfin
Subset sum and permutation sets

\leanhelper  For a subset $P\subseteq [n]$, define $\operatorname {sum}(P) = \sum _{i\in P} i$. 

For subsets $P,Q\subseteq [n]$, define $\operatorname {Perm}(P,Q) = \{ \sigma \in S_n : \sigma (P)=Q\} $ where $\sigma (P) = \{ \sigma (i) \mid i \in P\} $ denotes the image of $P$ under $\sigma $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.coeff
def.fps.coeff

If $n\in \mathbb {N}$, and if $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right) \in K\left[\left[x\right]\right]$ is an FPS, then we define an element $\left[x^{n}\right]\mathbf{a}\in K$ by 

\[  \left[x^{n}\right]\mathbf{a}:=a_{n}.  \]

 This is called the \emph{coefficient of }$x^{n}$\emph{ in }$\mathbf{a}$, or the $n$\emph{-th coefficient} of $\mathbf{a}$, or the $x^{n}$\emph{-coefficient} of $\mathbf{a}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.comps
def.fps.comps

\textbf{(a)} An \emph{(integer) composition} means a (finite) tuple of positive integers. \medskip 

\textbf{(b)} The \emph{size} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $\alpha _{1}+\alpha _{2}+\cdots +\alpha _{m}$. It is written $\left\vert \alpha \right\vert $. \medskip 

\textbf{(c)} The \emph{length} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $m$. It is written $\ell \left( \alpha \right) $. \medskip 

\textbf{(d)} Let $n\in \mathbb {N}$. A \emph{composition of }$n$ means a composition whose size is $n$. \medskip 

\textbf{(e)} Let $n\in \mathbb {N}$ and $k\in \mathbb {N}$. A \emph{composition of }$n$\emph{ into }$k$\emph{ parts} is a composition whose size is $n$ and whose length is $k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.fps
def.fps.fps

A \emph{formal power series} (or, short, \emph{FPS}) in $1$ indeterminate over $K$ means a sequence $\left(a_{0},a_{1},a_{2},\ldots \right) = \left(a_{n}\right)_{n\in \mathbb {N}} \in K^{\mathbb {N}}$ of elements of $K$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.ops
def.fps.ops

\textbf{(a)} The \emph{sum} of two FPSs $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right)$ and $\mathbf{b}=\left(b_{0},b_{1},b_{2},\ldots \right)$ is defined to be the FPS

\[  \left(a_{0}+b_{0},\  \  a_{1}+b_{1},\  \  a_{2}+b_{2},\  \  \ldots \right).  \]

 It is denoted by $\mathbf{a}+\mathbf{b}$. \medskip 

\textbf{(b)} The \emph{difference} of two FPSs $\mathbf{a}=\left(a_{0},a_{1},a_{2},\ldots \right)$ and $\mathbf{b}=\left(b_{0},b_{1},b_{2},\ldots \right)$ is defined to be the FPS

\[  \left(a_{0}-b_{0},\  \  a_{1}-b_{1},\  \  a_{2}-b_{2},\  \  \ldots \right).  \]

 It is denoted by $\mathbf{a}-\mathbf{b}$. \medskip 

\textbf{(c)} If $\lambda \in K$ and if $\mathbf{a}=\left(a_{0},a_{1},a_{2},\ldots \right)$ is an FPS, then we define an FPS 

\[  \lambda \mathbf{a}:=\left(\lambda a_{0},\lambda a_{1},\lambda a_{2},\ldots \right).  \]

\textbf{(d)} The \emph{product} of two FPSs $\mathbf{a}=\left(a_{0},a_{1},a_{2},\ldots \right)$ and $\mathbf{b}=\left(b_{0},b_{1},b_{2},\ldots \right)$ is defined to be the FPS $\left(c_{0},c_{1},c_{2},\ldots \right)$, where 

\begin{align*}  c_{n} &  =\sum _{i=0}^{n}a_{i}b_{n-i}=\sum _{\substack {\left(i,j\right) \in \mathbb {N}^{2};\\ \begin{bgroup} i+j=n

\end{bgroup}}}a_{i}b_{j}\\ &  =a_{0}b_{n}+a_{1}b_{n-1}+a_{2}b_{n-2}+\cdots +a_{n}b_{0}\  \  \  \  \  \  \  \  \  \  \text{for each }n\in \mathbb {N}. \end{align*}

 This product is denoted by $\mathbf{a}\cdot \mathbf{b}$ or just by $\mathbf{ab}$. \medskip 

\textbf{(e)} For each $a\in K$, we define $\underline{a}$ to be the FPS $\left(a,0,0,0,\ldots \right)$. An FPS of the form $\underline{a}$ for some $a\in K$ (that is, an FPS $\left(a_{0},a_{1},a_{2},\ldots \right)$ satisfying $a_{1}=a_{2}=a_{3}=\cdots =0$) is said to be \emph{constant}. \medskip 

\textbf{(f)} The set of all FPSs (in $1$ indeterminate over $K$) is denoted $K\left[\left[x\right]\right]$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.pol
def.fps.pol

\textbf{(a)} An FPS $a\in K\left[ \left[ x\right] \right] $ is said to be a \emph{polynomial} if all but finitely many $n\in \mathbb {N}$ satisfy $\left[ x^{n}\right] a=0$ (that is, if all but finitely many coefficients of $a$ are $0$). \medskip 

\textbf{(b)} We let $K\left[ x\right] $ be the set of all polynomials $a\in K\left[ \left[ x\right] \right] $. This set $K\left[ x\right] $ is a subring of $K\left[ \left[ x\right] \right] $ (according to Theorem \ref{thm.fps.pol.ring} below), and is called the \emph{univariate polynomial ring} over $K$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.x
def.fps.x

Let $x$ denote the FPS $\left(0,1,0,0,0,\ldots \right)$. In other words, let $x$ denote the FPS with $\left[x^{1}\right]x=1$ and $\left[x^{i}\right]x=0$ for all $i\neq 1$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.isdblocky
def.IsDBlocky

\leanhelper  A subset $S \subseteq \{ 0, \ldots , n-1\} $ is \emph{$d$-blocky} if $S \subseteq \{ 0, \ldots , n-1\} $ and for each block index $i \in \{ 0, \ldots , \lfloor n/d \rfloor - 1\} $, either all elements of $\{ id, id+1, \ldots , id+d-1\} $ are in $S$ or none are.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.ksubsets
def.kSubsets

\leanhelper  The set $\binom {[n]}{k}$ of $k$-element subsets of $\{ 0, \ldots , n-1\} $: 

\[  \binom {[n]}{k} := \bigl\{ S \subseteq \{ 0,\ldots ,n-1\}  : |S| = k\bigr\} .  \]

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.qbinomial
def.qBinomial

\leanhelper  The \emph{$q$-binomial coefficient} $\binom {n}{k}_q$ is the polynomial in $\mathbb {Z}[q]$ defined by 

\[  \binom {n}{k}_q := \sum _{\substack {S \subseteq \{ 0,\ldots ,n-1\}  \\ |S| = k}} q^{\, \operatorname {sum}(S) - (0 + 1 + \cdots + (k-1))},  \]

 where $\operatorname {sum}(S) = \sum _{x \in S} x$. This is the local definition used in the formalization; it agrees with Mathlib’s $q$-binomial coefficient (see Lemma~ \ref{lem.qBinomial_eq_canonical}).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.root-of-unity.prim
def.root-of-unity.prim

Let $K$ be a field. Let $d$ be a positive integer. 

\textbf{(a)} A \emph{$d$-th root of unity} in $K$ means an element $\omega $ of $K$ satisfying $\omega ^d = 1$. 

\textbf{(b)} A \emph{primitive $d$-th root of unity} in $K$ means an element $\omega $ of $K$ satisfying $\omega ^d = 1$ but $\omega ^i \neq 1$ for each $i \in \{ 1, 2, \ldots , d-1\} $. In other words, a primitive $d$-th root of unity in $K$ means an element of the multiplicative group $K^{\times }$ whose order is $d$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The binders exactly encode the blueprint setting: `\u2200 {K} [Field K] {\u03c9} {d}, IsPrimitiveRoot \u03c9 d \u2192 0 < d \u2192 \u2200 (n k : \u2115)`, matching \u201cLet K be a field, d a positive integer, and \u03c9 a primitive d-th root of unity. For n,k \u2208 \u2115.\u201d The summation range `blockySubsets d n k` unfolds to the `kSubsets n k` satisfying `IsDBlocky d n`, which matches the stated subsets `S \u2286 [n]`, `|S| = k`, that are d-blocky. The exponent `S.sum id - (Finset.range k).sum id` is precisely `sum(S) - (0+1+\u22ef+(k-1))`; natural subtraction causes no change on a k-element subset because its sum is at least that minimum. On the right, `\u2191((n / d).choose (k / d))` is the field-valued form of `binom(n/d,k/d)`, while `(Polynomial.aeval \u03c9) (qBinomial (n % d) (k % d))` is the local combinatorial q-binomial evaluated at \u03c9, exactly `binom(n mod d, k mod d)_\u03c9`. The formal `IsPrimitiveRoot` characterization is equivalent, for positive d in a field, to the blueprint\u2019s primitive-root definition."
}