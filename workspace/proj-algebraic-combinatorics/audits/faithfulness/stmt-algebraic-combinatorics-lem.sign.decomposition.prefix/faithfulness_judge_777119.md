## TARGET AlgebraicCombinatorics.CauchyBinet.sign_decomposition_prefix (theorem) — ELABORATED SIGNATURE
∀ {n k : ℕ} (hk : k ≤ n) (σ : Equiv.Perm (Fin n))
  (hσ :
    AlgebraicCombinatorics.CauchyBinet.imageFinset σ (AlgebraicCombinatorics.CauchyBinet.prefixFinset n k hk) =
      AlgebraicCombinatorics.CauchyBinet.prefixFinset n k hk),
  let P := AlgebraicCombinatorics.CauchyBinet.prefixFinset n k hk;
  ↑(Equiv.Perm.sign σ) =
    (-1) ^ (AlgebraicCombinatorics.CauchyBinet.finsetSumFin P + AlgebraicCombinatorics.CauchyBinet.finsetSumFin P) *
        ↑(Equiv.Perm.sign (AlgebraicCombinatorics.CauchyBinet.extractAlpha P P ⋯ σ hσ)) *
      ↑(Equiv.Perm.sign (AlgebraicCombinatorics.CauchyBinet.extractBeta P P ⋯ σ hσ))

Docstring: Base case of sign_decomposition: when P = Q = prefixFinset n k hk. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.imageFinset (def)
{n : ℕ} → Equiv.Perm (Fin n) → Finset (Fin n) → Finset (Fin n)

Body:
fun {n} σ P => Finset.map { toFun := ⇑σ, inj' := ⋯ } P

Docstring: The image of a finset under a permutation.

This is definitionally equal to `PermFinset.imageFinset` (see `imageFinset_eq_permFinset`).
New code should prefer `PermFinset.imageFinset`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.prefixFinset (def)
(n k : ℕ) → k ≤ n → Finset (Fin n)

Body:
fun n k _hk => {i | ↑i < k}

Docstring: The finset {0, 1, ..., k-1} ⊆ Fin n. 

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

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


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

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Units.val
{α : Type u} → [inst : Monoid α] → αˣ → α

Docstring: The underlying value in the base `Monoid`. 

## BASE-LIBRARY REF Int.instMonoid
Monoid ℤ

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

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

## BASE-LIBRARY REF MulOneClass.toMulOne
{M : Type u} → [self : MulOneClass M] → MulOne M

## BASE-LIBRARY REF Monoid.toMulOneClass
{M : Type u} → [self : Monoid M] → MulOneClass M

## BASE-LIBRARY REF DivInvMonoid.toMonoid
{G : Type u} → [self : DivInvMonoid G] → Monoid G

## BASE-LIBRARY REF Group.toDivInvMonoid
{G : Type u} → [self : Group G] → DivInvMonoid G

## BASE-LIBRARY REF Equiv.Perm.permGroup
{α : Type u_4} → Group (Equiv.Perm α)

## BASE-LIBRARY REF Units.instMulOneClass
{α : Type u} → [inst : Monoid α] → MulOneClass αˣ

Docstring: Units of a monoid have a multiplication and multiplicative identity. 

## BASE-LIBRARY REF MonoidHom.instFunLike
{M : Type u_4} → {N : Type u_5} → [inst : MulOne M] → [inst_1 : MulOne N] → FunLike (M →* N) M N

## BASE-LIBRARY REF Equiv.Perm.sign
{α : Type u} → [DecidableEq α] → [Fintype α] → Equiv.Perm α →* ℤˣ

Docstring: `SignType.sign` of a permutation returns the signature or parity of a permutation, `1` for even
permutations, `-1` for odd permutations. It is the unique surjective group homomorphism from
`Perm α` to the group with two elements. 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

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

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF Int.instNegInt
Neg ℤ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

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

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF rfl
∀ {α : Sort u} {a : α}, a = a

Docstring: `rfl : a = a` is the unique constructor of the equality type. This is the
same as `Eq.refl` except that it takes `a` implicitly instead of explicitly.

This is a more powerful theorem than it may appear at first, because although
the statement of the theorem is `a = a`, Lean will allow anything that is
definitionally equal to that type. So, for instance, `2 + 2 = 4` is proven in
Lean by `rfl`, because both sides are the same up to definitional equality.


## BASE-LIBRARY REF Compl.compl
{α : Type u_1} → [self : Compl α] → α → α

Docstring: Set / lattice complement 

Conventions for notations in identifiers:

 * The recommended spelling of `ᶜ` in identifiers is `compl`.

## BASE-LIBRARY REF BooleanAlgebra.toCompl
{α : Type u} → [self : BooleanAlgebra α] → Compl α

## BASE-LIBRARY REF Finset.booleanAlgebra
{α : Type u_1} → [Fintype α] → [DecidableEq α] → BooleanAlgebra (Finset α)

## BASE-LIBRARY REF Finset.map
{α : Type u_1} → {β : Type u_2} → (α ↪ β) → Finset α → Finset β

Docstring: When `f` is an embedding of `α` in `β` and `s` is a finset in `α`, then `s.map f` is the image
finset in `β`. The embedding condition guarantees that there are no duplicates in the image. 

## BASE-LIBRARY REF Function.Embedding.mk
{α : Sort u_1} → {β : Sort u_2} → (toFun : α → β) → Function.Injective toFun → α ↪ β

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## BASE-LIBRARY REF Nat.decLt
(n m : ℕ) → Decidable (n < m)

Docstring: A decision procedure for strict inequality of natural numbers, usually accessed via the
`DecidableLT Nat` instance.

Examples:
 * `(if 3 < 4 then "yes" else "no") = "yes"`
 * `(if 4 < 4 then "yes" else "no") = "no"`
 * `(if 6 < 4 then "yes" else "no") = "no"`
 * `show 5 < 12 by decide`


## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF OrderEmbedding
(α : Type u_6) → (β : Type u_7) → [LE α] → [LE β] → Type (max u_6 u_7)

Docstring: An order embedding is an embedding `f : α ↪ β` such that `a ≤ b ↔ (f a) ≤ (f b)`.
This definition is an abbreviation of `RelEmbedding (≤) (≤)`. 

## BASE-LIBRARY REF instLEFin
{n : ℕ} → LE (Fin n)

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

## BASE-LIBRARY REF Finset.orderEmbOfFin
{α : Type u_1} → [inst : LinearOrder α] → (s : Finset α) → {k : ℕ} → s.card = k → Fin k ↪o α

Docstring: Given a finset `s` of cardinality `k` in a linear order `α`, the map `orderEmbOfFin s h` is
the increasing bijection between `Fin k` and `s` as an order embedding into `α`. Here, `h` is a
proof that the cardinality of `s` is `k`. We use this instead of an embedding `Fin s.card ↪o α` to
avoid casting issues in further uses of this function. 

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Finset.instMembership
{α : Type u_1} → Membership α (Finset α)

## BASE-LIBRARY REF instFunLikeOrderEmbedding
(α : Type u_6) → (β : Type u_7) → [inst : LE α] → [inst_1 : LE β] → FunLike (α ↪o β) α β

## BASE-LIBRARY REF OrderIso
(α : Type u_6) → (β : Type u_7) → [LE α] → [LE β] → Type (max u_6 u_7)

Docstring: An order isomorphism is an equivalence such that `a ≤ b ↔ (f a) ≤ (f b)`.
This definition is an abbreviation of `RelIso (≤) (≤)`. 

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

## BASE-LIBRARY REF SetLike.instMembership
{A : Type u_1} → {B : Type u_2} → [i : SetLike A B] → Membership B A

## BASE-LIBRARY REF Finset.instSetLike
{α : Type u_1} → SetLike (Finset α) α

Docstring: Convert a finset to a set in the natural way. 

## BASE-LIBRARY REF Subtype.instLE
{α : Type u} → [LE α] → {P : α → Prop} → LE (Subtype P)

## BASE-LIBRARY REF Finset.orderIsoOfFin
{α : Type u_1} → [inst : LinearOrder α] → (s : Finset α) → {k : ℕ} → s.card = k → Fin k ≃o ↥s

Docstring: Given a finset `s` of cardinality `k` in a linear order `α`, the map `orderIsoOfFin s h`
is the increasing bijection between `Fin k` and `s` as an `OrderIso`. Here, `h` is a proof that
the cardinality of `s` is `k`. We use this instead of an iso `Fin s.card ≃o s` to avoid
casting issues in further uses of this function. 

## BASE-LIBRARY REF instFunLikeOrderIso
(α : Type u_6) → (β : Type u_7) → [inst : LE α] → [inst_1 : LE β] → FunLike (α ≃o β) α β

## BASE-LIBRARY REF OrderIso.symm
{α : Type u_2} → {β : Type u_3} → [inst : LE α] → [inst_1 : LE β] → α ≃o β → β ≃o α

Docstring: Inverse of an order isomorphism. 

## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

## BASE-LIBRARY REF Function.Injective
{α : Sort u_1} → {β : Sort u_2} → (α → β) → Prop

Docstring: A function `f : α → β` is called injective if `f x = f y` implies `x = y`. 

## BASE-LIBRARY REF Function.Surjective
{α : Sort u_1} → {β : Sort u_2} → (α → β) → Prop

Docstring: A function `f : α → β` is called surjective if every `b : β` is equal to `f a`
for some `a : α`. 

## BASE-LIBRARY REF Equiv.ofBijective
{α : Sort u} → {β : Sort v} → (f : α → β) → Function.Bijective f → α ≃ β

Docstring: If `f` is a bijective function, then its domain is equivalent to its codomain. 

## BASE-LIBRARY REF Matrix
Type u → Type u' → Type v → Type (max u u' v)

Docstring: `Matrix m n R` is the type of matrices with entries in `R`, whose rows are indexed by `m`
and whose columns are indexed by `n`. 

## BASE-LIBRARY REF Matrix.submatrix
{l : Type u_1} →
  {m : Type u_2} → {n : Type u_3} → {o : Type u_4} → {α : Type v} → Matrix m n α → (l → m) → (o → n) → Matrix l o α

Docstring: Given maps `(r : l → m)` and `(c : o → n)` reindexing the rows and columns of
a matrix `M : Matrix m n α`, the matrix `M.submatrix r c : Matrix l o α` is defined
by `(M.submatrix r c) i j = M (r i) (c j)` for `(i,j) : l × o`.
Note that the total number of row and columns does not have to be preserved. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Matrix.det
{n : Type u_2} → [DecidableEq n] → [Fintype n] → {R : Type v} → [CommRing R] → Matrix n n R → R

Docstring: The determinant of a matrix given by the Leibniz formula. 

## INFORMAL STATEMENT
Sign decomposition base case

\leanhelper  When $P = Q = [k]$ (the prefix finset), the sign decomposition formula 

\[  (-1)^{\sigma } = (-1)^{\operatorname {sum}[k]+\operatorname {sum}[k]} \cdot (-1)^{\alpha _\sigma }\cdot (-1)^{\beta _\sigma } = (-1)^{\alpha _\sigma }\cdot (-1)^{\beta _\sigma }  \]

 holds, where the sign factor vanishes because $\operatorname {sum}[k] + \operatorname {sum}[k] = k(k-1)$ is even.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv-2eb59533
conv-2eb59533

In the Lean formalization, we use $\operatorname {Fin} n = \{ 0, 1, \ldots , n-1\} $ instead of the textbook’s $[n] = \{ 1, 2, \ldots , n\} $. Both are $n$-element sets, so their symmetric groups are isomorphic. Permutations are represented by the type of bijections $X \to X$ (denoted $\operatorname {Equiv.Perm}\,  X$ in Lean), which is a group under composition. Composition $\alpha \beta $ is the group multiplication $\alpha * \beta $, sending $x$ to $\alpha (\beta (x))$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.det.sum-compl
conv.det.sum-compl

For any subset $I$ of $[n]$, we write $\widetilde{I} = [n] \setminus I$ for its complement, and $\operatorname {sum} S = \sum _{s \in S} s$ for any finite set $S$ of integers.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.det.imagefinset
def.det.imageFinset

\leanhelper  The \emph{image} of a finite subset $P \subseteq [n]$ under a permutation $\sigma \in S_n$ is $\sigma (P) = \{ \sigma (i) \mid i \in P\} $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.extract
Extraction of component permutations

\leanhelper  Let $P,Q\subseteq [n]$ with $|P|=|Q|=k$ and let $\sigma \in S_n$ satisfy $\sigma (P) = Q$. Write the elements of $P$ in increasing order as $p_1 < \cdots < p_k$, of $Q$ as $q_1 < \cdots < q_k$, of $\overline{P}$ as $p'_1 < \cdots < p'_\ell $, and of $\overline{Q}$ as $q'_1 < \cdots < q'_\ell $. 

Define $\alpha _\sigma \in S_k$ by $\sigma (p_i) = q_{\alpha _\sigma (i)}$ and $\beta _\sigma \in S_\ell $ by $\sigma (p'_i) = q'_{\beta _\sigma (i)}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.finsetsumfin
Subset sum and permutation sets

\leanhelper  For a subset $P\subseteq [n]$, define $\operatorname {sum}(P) = \sum _{i\in P} i$. 

For subsets $P,Q\subseteq [n]$, define $\operatorname {Perm}(P,Q) = \{ \sigma \in S_n : \sigma (P)=Q\} $ where $\sigma (P) = \{ \sigma (i) \mid i \in P\} $ denotes the image of $P$ under $\sigma $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.notations
def.perm.notations

Let $n \in \mathbb {N}$ and $\sigma \in S_n$. We introduce three notations for $\sigma $: 

\textbf{(a)} A \emph{two-line notation} of $\sigma $ means a $2 \times n$-array 

\[  \begin{pmatrix}  p_1 

&  p_2 

&  \cdots 

&  p_n 

\\ \sigma (p_1) 

&  \sigma (p_2) 

&  \cdots 

&  \sigma (p_n) 

\end{pmatrix},  \]

 where the entries $p_1, p_2, \ldots , p_n$ of the top row are the $n$ elements of $[n]$ in some order. Commonly, we pick $p_i = i$. 

\textbf{(b)} The \emph{one-line notation} (short, \emph{OLN}) of $\sigma $ means the $n$-tuple $(\sigma (1), \sigma (2), \ldots , \sigma (n))$. 

\textbf{(c)} The \emph{cycle digraph} of $\sigma $ is the directed graph with vertices $1, 2, \ldots , n$ and arcs $i \to \sigma (i)$ for all $i \in [n]$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.sn-iven
def.perm.Sn-iven

Let $n \in \mathbb {Z}$. Then, $[n]$ shall mean the set $\{ 1, 2, \ldots , n\} $. This is an $n$-element set if $n \ge 0$, and is an empty set if $n \le 0$. 

The symmetric group $S_{[n]}$ (consisting of all permutations of $[n]$) will be denoted $S_n$ and called the $n$\emph{-th symmetric group}. Its size is $n!$ (when $n \ge 0$).

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target quantifies `\u2200 {n k : \u2115} (hk : k \u2264 n) (\u03c3 : Equiv.Perm (Fin n))` and assumes `h\u03c3 : imageFinset \u03c3 (prefixFinset n k hk) = prefixFinset n k hk`, exactly the setting needed for the informal base case `P = Q = [k]` and for the definitions of `\u03b1_\u03c3` and `\u03b2_\u03c3`, which require `\u03c3(P)=Q`. The conclusion is the first displayed equality: `\u2191(Equiv.Perm.sign \u03c3) = (-1) ^ (finsetSumFin P + finsetSumFin P) * \u2191(sign (extractAlpha ...)) * \u2191(sign (extractBeta ...))`. Here `prefixFinset n k hk = {i : Fin n | i < k}` implements the stated zero-based Lean convention, while `extractAlpha` and `extractBeta` implement the component permutations using increasing order. Although the target does not explicitly include the final simplified equality, its exponent has the form `a + a`, hence is even, so `(-1)^(a+a)=1`; therefore the formal equality implies `sign \u03c3 = sign \u03b1_\u03c3 * sign \u03b2_\u03c3` as claimed. The binders `hk` and `h\u03c3` are not extraneous mathematical restrictions: they ensure that the prefix is a subset of `Fin n` and that the extracted component permutations in this `P=Q` case are defined."
}