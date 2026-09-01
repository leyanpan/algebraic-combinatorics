## TARGET AlgebraicCombinatorics.FPS.Laurent.kBoundedBTValue_mem_Icc (theorem) — ELABORATED SIGNATURE
∀ (k : ℕ),
  ∀ f ∈ AlgebraicCombinatorics.FPS.Laurent.kBoundedBTReps k,
    AlgebraicCombinatorics.FPS.Laurent.kBoundedBTValue k f ∈
      AlgebraicCombinatorics.FPS.Laurent.Icc_symm (AlgebraicCombinatorics.FPS.Laurent.maxBT k)

Docstring: The value of any k-bounded representation is in `[-M_k, M_k]`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.kBoundedBTReps (def)
(k : ℕ) → Finset (Fin (k + 1) → ℤ)

Body:
fun k => Fintype.piFinset fun x => AlgebraicCombinatorics.FPS.Laurent.btDigits

Docstring: A k-bounded balanced ternary representation is a function `f : Fin (k+1) → {-1, 0, 1}`.

These are representations where `f(i) = 0` for all `i > k`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.Icc_symm (def)
ℕ → Finset ℤ

Body:
fun M => Finset.Icc (-↑M) ↑M

Docstring: The set of integers from -M to M. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.maxBT (def)
ℕ → ℕ

Body:
fun k => ∑ i ∈ Finset.range (k + 1), 3 ^ i

Docstring: The maximum absolute value representable with k+1 balanced ternary digits:
`M_k = 3^0 + 3^1 + ... + 3^k = (3^{k+1} - 1) / 2` 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.kBoundedBTValue (def)
(k : ℕ) → (Fin (k + 1) → ℤ) → ℤ

Body:
fun k f => ∑ i, f i * 3 ^ ↑i

Docstring: The value of a k-bounded balanced ternary representation. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.btDigits (def)
Finset ℤ

Body:
{-1, 0, 1}

Docstring: The set of balanced ternary digits {-1, 0, 1}. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Finset.instMembership
{α : Type u_1} → Membership α (Finset α)

## BASE-LIBRARY REF Fintype.piFinset
{α : Type u_1} → [DecidableEq α] → [Fintype α] → {δ : α → Type u_4} → ((a : α) → Finset (δ a)) → Finset ((a : α) → δ a)

Docstring: Given for all `a : α` a finset `t a` of `δ a`, then one can define the
finset `Fintype.piFinset t` of all functions taking values in `t a` for all `a`. This is the
analogue of `Finset.pi` where the base finset is `univ` (but formally they are not the same, as
there is an additional condition `i ∈ Finset.univ` in the `Finset.pi` definition). 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Finset.Icc
{α : Type u_1} → [inst : Preorder α] → [LocallyFiniteOrder α] → α → α → Finset α

Docstring: The finset $[a, b]$ of elements `x` such that `a ≤ x` and `x ≤ b`. Basically `Set.Icc a b` as a
finset. 

## BASE-LIBRARY REF PartialOrder.toPreorder
{α : Type u_2} → [self : PartialOrder α] → Preorder α

## BASE-LIBRARY REF SemilatticeInf.toPartialOrder
{α : Type u} → [self : SemilatticeInf α] → PartialOrder α

## BASE-LIBRARY REF Lattice.toSemilatticeInf
{α : Type u} → [self : Lattice α] → SemilatticeInf α

## BASE-LIBRARY REF instLatticeInt
Lattice ℤ

## BASE-LIBRARY REF Int.instLocallyFiniteOrder
LocallyFiniteOrder ℤ

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF Int.instNegInt
Neg ℤ

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


## BASE-LIBRARY REF instNatCastInt
NatCast ℤ

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Docstring: `range n` is the set of natural numbers less than `n`. 

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

## BASE-LIBRARY REF Nat.instMonoid
Monoid ℕ

## BASE-LIBRARY REF Int.instAddCommMonoid
AddCommMonoid ℤ

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF Int.instMul
Mul ℤ

## BASE-LIBRARY REF Int.instMonoid
Monoid ℤ

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## BASE-LIBRARY REF Insert.insert
{α : outParam (Type u)} → {γ : Type v} → [self : Insert α γ] → α → γ → γ

Docstring: `insert x xs` inserts the element `x` into the collection `xs`. 

## BASE-LIBRARY REF Finset.instInsert
{α : Type u_1} → [DecidableEq α] → Insert α (Finset α)

Docstring: `insert a s` is the set `{a} ∪ s` containing `a` and the elements of `s`. 

## BASE-LIBRARY REF Int.instDecidableEq
DecidableEq ℤ

Docstring: Decides whether two integers are equal. Usually accessed via the `DecidableEq Int` instance.

This function is overridden by the compiler with an efficient implementation. This definition is the
logical model.

Examples:
* `show (7 : Int) = (3 : Int) + (4 : Int) by decide`
* `if (6 : Int) = (3 : Int) * (2 : Int) then "yes" else "no" = "yes"`
* `(¬ (6 : Int) = (3 : Int)) = true`


## BASE-LIBRARY REF Singleton.singleton
{α : outParam (Type u)} → {β : Type v} → [self : Singleton α β] → α → β

Docstring: `singleton x` is a collection with the single element `x` (notation: `{x}`). 

Conventions for notations in identifiers:

 * The recommended spelling of `{x}` in identifiers is `singleton`.

## BASE-LIBRARY REF Finset.instSingleton
{α : Type u_1} → Singleton α (Finset α)

Docstring: `{a} : Finset a` is the set `{a}` containing `a` and nothing else.

This differs from `insert a ∅` in that it does not require a `DecidableEq` instance for `α`.


## INFORMAL STATEMENT
Bounded representation values lie in [-Mk, Mk]

$}]   \leanhelper  The value $\sum _{i=0}^{k} f(i) \cdot 3^i$ of any $k$-bounded balanced ternary representation $f$ (with $f(i) \in \{ -1, 0, 1\} $) lies in the interval $[-M_k, M_k]$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.laure.balanced-tern
def.fps.laure.balanced-tern

\leanhelper  A \emph{balanced ternary representation} of an integer $n$ means an essentially finite sequence $\left( b_{i}\right) _{i\in \mathbb {N}}=\left( b_{0},b_{1},b_{2},\ldots \right) \in \left\{  0,1,-1\right\}  ^{\mathbb {N}}$ such that

\[  n=\sum _{i\in \mathbb {N}}b_{i}3^{i}.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.laure.binary-rep
def.fps.laure.binary-rep

\leanhelper  A \emph{binary representation} of an integer $n$ means an essentially finite sequence $\left( b_{i}\right) _{i\in \mathbb {N}}=\left( b_{0},b_{1},b_{2},\ldots \right) \in \left\{  0,1\right\}  ^{\mathbb {N}}$ such that

\[  n=\sum _{i\in \mathbb {N}}b_{i}2^{i}.  \]

 (Recall that “essentially finite” means “all but finitely many $i\in \mathbb {N}$ satisfy $b_{i}=0$”.)

## VERDICT
{
  "verdict": "faithful",
  "justification": "The signature quantifies over exactly the required data: `\u2200 (k : \u2115), \u2200 f \u2208 kBoundedBTReps k`, where `kBoundedBTReps k` consists of functions `Fin (k + 1) \u2192 \u2124` whose values lie in `btDigits = {-1, 0, 1}`. This matches \u201cany k-bounded balanced ternary representation f (with f(i) \u2208 {-1, 0, 1})\u201d; the finite domain represents indices `0,\u2026,k`, equivalently extending the sequence by zero above k. The formal value `kBoundedBTValue k f = \u2211 i, f i * 3 ^ \u2191i` is therefore exactly `\u2211_{i=0}^k f(i)\u00b73^i`. Finally, `maxBT k = \u2211 i \u2208 Finset.range (k + 1), 3 ^ i` and `Icc_symm (maxBT k) = Finset.Icc (-\u2191(maxBT k)) \u2191(maxBT k)`, so the conclusion says precisely that the value lies in `[-M_k, M_k]`. No additional mathematical hypothesis or narrowed range is present."
}