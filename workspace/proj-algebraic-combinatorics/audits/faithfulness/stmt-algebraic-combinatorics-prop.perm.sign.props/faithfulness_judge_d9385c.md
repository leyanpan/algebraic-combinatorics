## TARGET Equiv.Perm.sign_transposition (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_1} [inst : DecidableEq α] [inst_1 : Fintype α] {x y : α}, x ≠ y → Equiv.Perm.sign (Equiv.swap x y) = -1

Docstring: **(b)** The sign of a transposition is -1.
**Proposition (prop.perm.sign.props)(b)** 

## TARGET Equiv.Perm.sign_mul' (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_1} [inst : DecidableEq α] [inst_1 : Fintype α] (σ τ : Equiv.Perm α),
  Equiv.Perm.sign (σ * τ) = Equiv.Perm.sign σ * Equiv.Perm.sign τ

Docstring: **(d)** The sign is multiplicative: sign(στ) = sign(σ) · sign(τ).
**Proposition (prop.perm.sign.props)(d)** 

## TARGET Equiv.Perm.sign_prod_list (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_1} [inst : DecidableEq α] [inst_1 : Fintype α] (l : List (Equiv.Perm α)),
  Equiv.Perm.sign l.prod = (List.map (⇑Equiv.Perm.sign) l).prod

Docstring: **(e)** The sign of a product equals the product of signs.
**Proposition (prop.perm.sign.props)(e)** 

## TARGET Equiv.Perm.prod_diff_comp_perm (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} {R : Type u_2} [inst : CommRing R] (σ : Equiv.Perm (Fin n)) (x : Fin n → R),
  ∏ i, ∏ j ∈ Finset.Ioi i, (x (σ i) - x (σ j)) = ↑↑(Equiv.Perm.sign σ) * ∏ i, ∏ j ∈ Finset.Ioi i, (x i - x j)

Docstring: **(h)** Product of differences under permutation.
**Proposition (prop.perm.sign.props)(h)**

For any elements x₁, ..., xₙ of a commutative ring and σ ∈ Sₙ:
∏_{i < j} (x_{σ(i)} - x_{σ(j)}) = sign(σ) · ∏_{i < j} (xᵢ - xⱼ)


## TARGET Equiv.Perm.sign_inv' (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_1} [inst : DecidableEq α] [inst_1 : Fintype α] (σ : Equiv.Perm α), Equiv.Perm.sign σ⁻¹ = Equiv.Perm.sign σ

Docstring: **(f)** The sign of the inverse equals the sign of the permutation.
**Proposition (prop.perm.sign.props)(f)** 

## TARGET Equiv.Perm.sign_id (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_1} [inst : DecidableEq α] [inst_1 : Fintype α], Equiv.Perm.sign 1 = 1

Docstring: **(a)** The sign of the identity permutation is 1.
**Proposition (prop.perm.sign.props)(a)** 

## TARGET Equiv.Perm.sign_isCycle (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_1} [inst : DecidableEq α] [inst_1 : Fintype α] {σ : Equiv.Perm α},
  σ.IsCycle → Equiv.Perm.sign σ = -(-1) ^ σ.support.card

Docstring: **(c)** The sign of a k-cycle is (-1)^(k-1).
**Proposition (prop.perm.sign.props)(c)**

This follows from the fact that a k-cycle has support of size k and
sign(σ) = -(-1)^|support(σ)| for cycles. 

## TARGET Equiv.Perm.sign_eq_prod_pairs (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (σ : Equiv.Perm (Fin n)), Equiv.Perm.sign σ = ∏ i, ∏ j ∈ Finset.Ioi i, if σ i < σ j then 1 else -1

Docstring: **(g)** Sign as a product over pairs.
**Proposition (prop.perm.sign.props)(g)**

For σ ∈ Sₙ: sign(σ) = ∏_{1 ≤ i < j ≤ n} (σ(i) - σ(j)) / (i - j)

We state this in a slightly different but equivalent form using the indicator function. 

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF Fintype
Type u_4 → Type u_4

Docstring: `Fintype α` means that `α` is finite, i.e. there are only
finitely many distinct elements of type `α`. The evidence of this
is a finset `elems` (a list up to permutation without duplicates),
together with a proof that everything of type `α` is in the list. 

## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

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

## BASE-LIBRARY REF Units
(α : Type u) → [Monoid α] → Type u

Docstring: Units of a `Monoid`, bundled version. Notation: `αˣ`.

An element of a `Monoid` is a unit if it has a two-sided inverse.
This version bundles the inverse element so that it can be computed.
For a predicate see `IsUnit`. 

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


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


## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

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

## BASE-LIBRARY REF Equiv.swap
{α : Sort u_1} → [DecidableEq α] → α → α → Equiv.Perm α

Docstring: `swap a b` is the permutation that swaps `a` and `b` and
leaves other values as is. 

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF Units.instNeg
{α : Type u} → [inst : Monoid α] → [HasDistribNeg α] → Neg αˣ

Docstring: Each element of the group of units of a ring has an additive inverse. 

## BASE-LIBRARY REF NonUnitalNonAssocRing.toHasDistribNeg
{α : Type u} → [inst : NonUnitalNonAssocRing α] → HasDistribNeg α

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF NonUnitalNormedCommRing.toNonUnitalCommRing
{α : Type u_5} → [self : NonUnitalNormedCommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF NormedCommRing.toNonUnitalNormedCommRing
{α : Type u_2} → [β : NormedCommRing α] → NonUnitalNormedCommRing α

Docstring: A normed commutative ring is a non-unital normed commutative ring. 

## BASE-LIBRARY REF Int.instNormedCommRing
NormedCommRing ℤ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF Units.instOne
{α : Type u} → [inst : Monoid α] → One αˣ

Docstring: Units of a monoid have a unit 

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF Equiv.Perm.instMul
{α : Type u_4} → Mul (Equiv.Perm α)

## BASE-LIBRARY REF Units.instMul
{α : Type u} → [inst : Monoid α] → Mul αˣ

Docstring: Units of a monoid have an induced multiplication. 

## BASE-LIBRARY REF List
Type u → Type u

Docstring: Linked lists: ordered lists, in which each element has a reference to the next element.

Most operations on linked lists take time proportional to the length of the list, because each
element must be traversed to find the next element.

`List α` is isomorphic to `Array α`, but they are useful for different things:
* `List α` is easier for reasoning, and `Array α` is modeled as a wrapper around `List α`.
* `List α` works well as a persistent data structure, when many copies of the tail are shared. When
  the value is not shared, `Array α` will have better performance because it can do destructive
  updates.


## BASE-LIBRARY REF List.prod
{α : Type u_1} → [Mul α] → [One α] → List α → α

Docstring: Computes the product of the elements of a list.

Examples:

[a, b, c].prod = a * (b * (c * 1))
[2, 3, 5].prod = 30


## BASE-LIBRARY REF Equiv.Perm.instOne
{α : Type u_4} → One (Equiv.Perm α)

## BASE-LIBRARY REF List.map
{α : Type u_1} → {β : Type u_2} → (α → β) → List α → List β

Docstring: Applies a function to each element of the list, returning the resulting list of values.

`O(|l|)`.

Examples:
* `[a, b, c].map f = [f a, f b, f c]`
* `[].map Nat.succ = []`
* `["one", "two", "three"].map (·.length) = [3, 3, 5]`
* `["one", "two", "three"].map (·.reverse) = ["eno", "owt", "eerht"]`


## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF CommRing.toCommMonoid
{α : Type u} → [self : CommRing α] → CommMonoid α

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Finset.Ioi
{α : Type u_1} → [inst : Preorder α] → [LocallyFiniteOrderTop α] → α → Finset α

Docstring: The finset $(a, ∞)$ of elements `x` such that `a < x`. Basically `Set.Ioi a` as a finset. 

## BASE-LIBRARY REF PartialOrder.toPreorder
{α : Type u_2} → [self : PartialOrder α] → Preorder α

## BASE-LIBRARY REF Fin.instPartialOrder
{n : ℕ} → PartialOrder (Fin n)

## BASE-LIBRARY REF Fin.instLocallyFiniteOrderTop
(n : ℕ) → LocallyFiniteOrderTop (Fin n)

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF SubNegMonoid.toSub
{G : Type u} → [self : SubNegMonoid G] → Sub G

## BASE-LIBRARY REF AddGroup.toSubNegMonoid
{A : Type u} → [self : AddGroup A] → SubNegMonoid A

## BASE-LIBRARY REF AddGroupWithOne.toAddGroup
{R : Type u} → [self : AddGroupWithOne R] → AddGroup R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF CommRing.toRing
{α : Type u} → [self : CommRing α] → Ring α

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

## BASE-LIBRARY REF Distrib.toMul
{R : Type u_1} → [self : Distrib R] → Mul R

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toDistrib
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → Distrib α

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF Int.cast
{R : Type u} → [IntCast R] → ℤ → R

Docstring: The canonical homomorphism `Int → R`. In most use cases, the target type will have a ring structure,
and this homomorphism should be a ring homomorphism.

`IntCast` and `NatCast` exist to allow different libraries with their own types that can be notated
as natural numbers to have consistent `simp` normal forms without needing to create coercion
simplification sets that are aware of all combinations. Libraries should make it easy to work with
`IntCast` where possible. For instance, in Mathlib there will be such a homomorphism (and thus an
`IntCast R` instance) whenever `R` is an additive group with a `1`.


## BASE-LIBRARY REF AddGroupWithOne.toIntCast
{R : Type u} → [self : AddGroupWithOne R] → IntCast R

## BASE-LIBRARY REF Units.val
{α : Type u} → [inst : Monoid α] → αˣ → α

Docstring: The underlying value in the base `Monoid`. 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Inv.inv
{α : Type u} → [self : Inv α] → α → α

Docstring: `a⁻¹` computes the inverse of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `⁻¹` in identifiers is `inv`.

## BASE-LIBRARY REF Equiv.Perm.instInv
{α : Type u_4} → Inv (Equiv.Perm α)

## BASE-LIBRARY REF Equiv.Perm.IsCycle
{α : Type u_2} → Equiv.Perm α → Prop

Docstring: A cycle is a non-identity permutation where any two nonfixed points of the permutation are
related by repeated application of the permutation. 

## BASE-LIBRARY REF HPow.hPow
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HPow α β γ] → α → β → γ

Docstring: `a ^ b` computes `a` to the power of `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `^` in identifiers is `pow`.

## BASE-LIBRARY REF instHPow
{α : Type u_1} → {β : Type u_2} → [Pow α β] → HPow α β α

## BASE-LIBRARY REF Int.instUnitsPow
{R : Type u_1} → [inst : CommSemiring R] → [_root_.Module R (Additive ℤˣ)] → Pow ℤˣ R

Docstring: There is a canonical power operation on `ℤˣ` by `R` if `Additive ℤˣ` is an `R`-module.

In lemma names, this operation is called `uzpow` to match `zpow`.

Notably this is satisfied by `R ∈ {ℕ, ℤ, ZMod 2}`. 

## BASE-LIBRARY REF Nat.instCommSemiring
CommSemiring ℕ

## BASE-LIBRARY REF AddCommMonoid.toNatModule
{M : Type u_3} → [inst : AddCommMonoid M] → _root_.Module ℕ M

## BASE-LIBRARY REF Additive
Type u_1 → Type u_1

Docstring: If `α` carries some multiplicative structure, then `Additive α` carries the corresponding
additive structure. 

## BASE-LIBRARY REF Additive.addCommMonoid
{α : Type u} → [CommMonoid α] → AddCommMonoid (Additive α)

## BASE-LIBRARY REF CommGroup.toCommMonoid
{G : Type u} → [self : CommGroup G] → CommMonoid G

## BASE-LIBRARY REF Units.instCommGroupUnits
{α : Type u_1} → [inst : CommMonoid α] → CommGroup αˣ

Docstring: Units of a commutative monoid form a commutative group. 

## BASE-LIBRARY REF Int.instCommMonoid
CommMonoid ℤ

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Equiv.Perm.support
{α : Type u_1} → [DecidableEq α] → [Fintype α] → Equiv.Perm α → Finset α

Docstring: The `Finset` of nonfixed points of a permutation. 

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTFin
{n : ℕ} → LT (Fin n)

## BASE-LIBRARY REF Fin.decLt
{n : ℕ} → (a b : Fin n) → Decidable (a < b)

## INFORMAL STATEMENT
prop.perm.sign.props

Let $n \in \mathbb {N}$. 

\textbf{(a)} The sign of the identity permutation $\operatorname {id} \in S_n$ is $(-1)^{\operatorname {id}} = 1$. 

\textbf{(b)} For any two distinct elements $i$ and $j$ of $[n]$, the transposition $t_{i,j} \in S_n$ has sign $(-1)^{t_{i,j}} = -1$. 

\textbf{(c)} For any positive integer $k$ and any distinct elements $i_1, i_2, \ldots , i_k \in [n]$, the $k$-cycle $\operatorname {cyc}_{i_1, i_2, \ldots , i_k}$ has sign $(-1)^{\operatorname {cyc}_{i_1, i_2, \ldots , i_k}} = (-1)^{k-1}$. 

\textbf{(d)} We have $(-1)^{\sigma \tau } = (-1)^{\sigma } \cdot (-1)^{\tau }$ for any $\sigma \in S_n$ and $\tau \in S_n$. 

\textbf{(e)} We have $(-1)^{\sigma _1 \sigma _2 \cdots \sigma _p} = (-1)^{\sigma _1} (-1)^{\sigma _2} \cdots (-1)^{\sigma _p}$ for any $\sigma _1, \sigma _2, \ldots , \sigma _p \in S_n$. 

\textbf{(f)} We have $(-1)^{\sigma ^{-1}} = (-1)^{\sigma }$ for any $\sigma \in S_n$. (The left hand side here has to be understood as $(-1)^{(\sigma ^{-1})}$.) 

\textbf{(g)} We have 

\[  (-1)^{\sigma } = \prod _{1 \leq i < j \leq n} \frac{\sigma (i) - \sigma (j)}{i - j} \qquad \text{for each } \sigma \in S_n.  \]

 (The product sign “$\prod _{1 \leq i < j \leq n}$” means a product over all pairs $(i,j)$ of integers satisfying $1 \leq i < j \leq n$. There are $\binom {n}{2}$ such pairs.) 

\textbf{(h)} If $x_1, x_2, \ldots , x_n$ are any elements of some commutative ring, and if $\sigma \in S_n$, then 

\[  \prod _{1 \leq i < j \leq n} \left( x_{\sigma (i)} - x_{\sigma (j)} \right) = (-1)^{\sigma } \prod _{1 \leq i < j \leq n} \left( x_i - x_j \right).  \]

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.cycs
def.perm.cycs

Let $X$ be a set. Let $i_1, i_2, \ldots , i_k$ be $k$ distinct elements of $X$. Then, 

\[  \operatorname {cyc}_{i_1, i_2, \ldots , i_k}  \]

 means the permutation of $X$ that sends 

\begin{align*} & i_1 \text{ to } i_2, \\ & i_2 \text{ to } i_3, \\ & \ldots , \\ & i_{k-1} \text{ to } i_k, \\ & i_k \text{ to } i_1 \end{align*}

 and leaves all other elements of $X$ unchanged. In other words, $\operatorname {cyc}_{i_1, i_2, \ldots , i_k}$ means the permutation of $X$ that satisfies 

\[  \operatorname {cyc}_{i_1, \ldots , i_k}(p) = \begin{cases}  i_{j+1}, &  \text{if } p = i_j \text{ for some } j \in \{ 1, 2, \ldots , k\} ;\\ p, &  \text{otherwise} \end{cases}  \]

 for every $p \in X$, where $i_{k+1}$ means $i_1$. 

This permutation is called a $k$\emph{-cycle}.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.tij
def.perm.tij

Let $i$ and $j$ be two distinct elements of a set $X$. 

Then, the \emph{transposition} $t_{i,j}$ is the permutation of $X$ that sends $i$ to $j$, sends $j$ to $i$, and leaves all other elements of $X$ unchanged.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The declarations jointly imply all eight parts. Parts (a), (b), (d), (e), and (f) directly match respectively `sign 1 = 1`, `x \u2260 y \u2192 sign (swap x y) = -1`, `sign (\u03c3 * \u03c4) = sign \u03c3 * sign \u03c4`, `sign l.prod = (l.map sign).prod`, and `sign \u03c3\u207b\u00b9 = sign \u03c3`. Their binders `{\u03b1} [DecidableEq \u03b1] [Fintype \u03b1]` are more general than the blueprint\u2019s `S_n`; `DecidableEq` is computational encoding, and every `Fin n` supplies both instances. For (c), `\u03c3.IsCycle \u2192 sign \u03c3 = -(-1) ^ \u03c3.support.card` gives `(-1)^(k-1)` for every nontrivial k-cycle because `-(-1)^k = (-1)^(k-1)`; the blueprint\u2019s exceptional positive case `k = 1`, whose cycle is the identity, is covered jointly by `sign_id`. Part (g), `\u220f i, \u220f j \u2208 Finset.Ioi i, if \u03c3 i < \u03c3 j then 1 else -1`, is the stated equivalent inversion-indicator form of the ratio product: each non-inversion contributes `1` and each inversion `-1`. Using `Fin n` rather than `[n]` merely shifts indices from `1,\u2026,n` to `0,\u2026,n-1`. Part (h) exactly quantifies `(R : Type) [CommRing R]`, `\u03c3 : Perm (Fin n)`, and `x : Fin n \u2192 R`, and its nested `Ioi` products are precisely over `i < j`; the coercion `\u2191\u2191(sign \u03c3)` represents the integer sign as an element of `R`. The base-library `Equiv.Perm.sign` is documented as parity, `1` for even and `-1` for odd, agreeing with the informal inversion-parity definition."
}