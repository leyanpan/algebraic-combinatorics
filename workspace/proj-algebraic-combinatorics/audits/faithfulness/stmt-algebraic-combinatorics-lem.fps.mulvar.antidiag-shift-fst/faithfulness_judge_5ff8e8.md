## TARGET AlgebraicCombinatorics.antidiag_shift_fst (theorem) — ELABORATED SIGNATURE
∀ {σ : Type u_2} [inst : DecidableEq σ] (i : σ) (m : σ →₀ ℕ),
  Finset.map { toFun := fun p => (p.1 + fun₀ | i => 1, p.2), inj' := ⋯ } (Finset.antidiagonal m) =
    {p ∈ Finset.antidiagonal (m + fun₀ | i => 1) | (fun₀ | i => 1) ≤ p.1}

Docstring: The map `(a, b) ↦ (a + single i 1, b)` gives a bijection from `antidiagonal m` to
the subset of `antidiagonal (m + single i 1)` where `single i 1 ≤ a`. 

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF Finsupp
Type u_9 → (M : Type u_10) → [Zero M] → Type (max u_10 u_9)

Docstring: `Finsupp α M`, denoted `α →₀ M`, is the type of functions `f : α → M` such that
`f x = 0` for all but finitely many `x`. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

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

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF Finset.map
{α : Type u_1} → {β : Type u_2} → (α ↪ β) → Finset α → Finset β

Docstring: When `f` is an embedding of `α` in `β` and `s` is a finset in `α`, then `s.map f` is the image
finset in `β`. The embedding condition guarantees that there are no duplicates in the image. 

## BASE-LIBRARY REF Function.Embedding.mk
{α : Sort u_1} → {β : Sort u_2} → (toFun : α → β) → Function.Injective toFun → α ↪ β

## BASE-LIBRARY REF Prod.mk
{α : Type u} → {β : Type v} → α → β → α × β

Docstring: Constructs a pair. This is usually written `(x, y)` instead of `Prod.mk x y`.


Conventions for notations in identifiers:

 * The recommended spelling of `(a, b)` in identifiers is `mk`.

## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF Finsupp.instAdd
{ι : Type u_1} → {M : Type u_3} → [inst : AddZeroClass M] → Add (ι →₀ M)

## BASE-LIBRARY REF AddMonoid.toAddZeroClass
{M : Type u} → [self : AddMonoid M] → AddZeroClass M

## BASE-LIBRARY REF Nat.instAddMonoid
AddMonoid ℕ

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

## BASE-LIBRARY REF Finsupp.single
{α : Type u_1} → {M : Type u_5} → [inst : Zero M] → α → M → α →₀ M

Docstring: `single a b` is the finitely supported function with value `b` at `a` and zero otherwise. 

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

## BASE-LIBRARY REF add_right_cancel
∀ {G : Type u_1} [inst : Add G] [IsRightCancelAdd G] {a b c : G}, a + b = c + b → a = c

## BASE-LIBRARY REF Finsupp.instIsRightCancelAdd
∀ {ι : Type u_1} {M : Type u_3} [inst : AddZeroClass M] [IsRightCancelAdd M], IsRightCancelAdd (ι →₀ M)

## BASE-LIBRARY REF AddRightCancelSemigroup.toIsRightCancelAdd
∀ {G : Type u} [self : AddRightCancelSemigroup G], IsRightCancelAdd G

Docstring: Any `AddRightCancelSemigroup` satisfies `IsRightCancelAdd`. 

## BASE-LIBRARY REF AddRightCancelMonoid.toAddRightCancelSemigroup
{M : Type u} → [self : AddRightCancelMonoid M] → AddRightCancelSemigroup M

## BASE-LIBRARY REF AddCancelMonoid.toAddRightCancelMonoid
{M : Type u} → [self : AddCancelMonoid M] → AddRightCancelMonoid M

## BASE-LIBRARY REF AddCancelCommMonoid.toAddCancelMonoid
(M : Type u) → [AddCancelCommMonoid M] → AddCancelMonoid M

## BASE-LIBRARY REF Nat.instAddCancelCommMonoid
AddCancelCommMonoid ℕ

## BASE-LIBRARY REF And.left
∀ {a b : Prop}, a ∧ b → a

Docstring: Extract the left conjunct from a conjunction. `h : a ∧ b` then
`h.left`, also notated as `h.1`, is a proof of `a`. 

## BASE-LIBRARY REF Eq.mp
{α β : Sort u} → α = β → α → β

Docstring: If `h : α = β` is a proof of type equality, then `h.mp : α → β` is the induced
"cast" operation, mapping elements of `α` to elements of `β`.

You can prove theorems about the resulting element by induction on `h`, since
`rfl.mp` is definitionally the identity function.


## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF Prod.mk.injEq
∀ {α : Type u} {β : Type v} (fst : α) (snd : β) (fst_1 : α) (snd_1 : β),
  ((fst, snd) = (fst_1, snd_1)) = (fst = fst_1 ∧ snd = snd_1)

## BASE-LIBRARY REF And.right
∀ {a b : Prop}, a ∧ b → b

Docstring: Extract the right conjunct from a conjunction. `h : a ∧ b` then
`h.right`, also notated as `h.2`, is a proof of `b`. 

## BASE-LIBRARY REF Prod.ext
∀ {α : Type u} {β : Type v} {x y : α × β}, x.1 = y.1 → x.2 = y.2 → x = y

## BASE-LIBRARY REF Finsupp.ext
∀ {α : Type u_1} {M : Type u_4} [inst : Zero M] {f g : α →₀ M}, (∀ (a : α), f a = g a) → f = g

## BASE-LIBRARY REF of_eq_true
∀ {p : Prop}, p = True → p

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF Finsupp.instFunLike
{α : Type u_1} → {M : Type u_4} → [inst : Zero M] → FunLike (α →₀ M) α M

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


## BASE-LIBRARY REF eq_self
∀ {α : Sort u_1} (a : α), (a = a) = True

## BASE-LIBRARY REF Finset.HasAntidiagonal.antidiagonal
{A : Type u_1} → {inst : AddMonoid A} → [self : Finset.HasAntidiagonal A] → A → Finset (A × A)

Docstring: The antidiagonal of an element `n` is the finset of pairs `(i, j)` such that `i + j = n`. 

## BASE-LIBRARY REF Finsupp.instAddMonoid
{ι : Type u_1} → {M : Type u_3} → [inst : AddMonoid M] → AddMonoid (ι →₀ M)

## BASE-LIBRARY REF Finsupp.instHasAntidiagonal
{α : Type u} → [DecidableEq α] → Finset.HasAntidiagonal (α →₀ ℕ)

Docstring: The antidiagonal of `s : α →₀ ℕ` is the finset of all pairs `(t₁, t₂) : (α →₀ ℕ) × (α →₀ ℕ)`
such that `t₁ + t₂ = s`. 

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF Finsupp.instLE
{ι : Type u_1} → {M : Type u_2} → [inst : Zero M] → [LE M] → LE (ι →₀ M)

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Finsupp.decidableLE
{ι : Type u_1} →
  {α : Type u_3} →
    [inst : AddCommMonoid α] →
      [inst_1 : PartialOrder α] → [CanonicallyOrderedAdd α] → [DecidableLE α] → DecidableLE (ι →₀ α)

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF Nat.instPartialOrder
PartialOrder ℕ

## BASE-LIBRARY REF Nat.instCanonicallyOrderedAdd
CanonicallyOrderedAdd ℕ

## BASE-LIBRARY REF Nat.decLe
(n m : ℕ) → Decidable (n ≤ m)

Docstring: A decision procedure for non-strict inequality of natural numbers, usually accessed via the
`DecidableLE Nat` instance.

Examples:
 * `(if 3 ≤ 4 then "yes" else "no") = "yes"`
 * `(if 6 ≤ 4 then "yes" else "no") = "no"`
 * `show 12 ≤ 12 by decide`
 * `show 5 ≤ 12 by decide`


## INFORMAL STATEMENT
lem.fps.mulvar.antidiag-shift-fst

\leanhelper  The map $(\mathbf{a}, \mathbf{b}) \mapsto (\mathbf{a} + \mathbf{e}_i, \mathbf{b})$ gives a bijection from $\operatorname {antidiagonal}(\mathbf{m})$ to the subset of $\operatorname {antidiagonal}(\mathbf{m} + \mathbf{e}_i)$ consisting of pairs $(\mathbf{a}, \mathbf{b})$ with $\mathbf{e}_i \leq \mathbf{a}$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal map `fun p => (p.1 + fun\u2080 | i => 1, p.2)` is exactly the informal map `(a, b) \u21a6 (a + e_i, b)`, with `fun\u2080 | i => 1` representing the finitely supported unit vector `e_i`. The equality identifies its image of `Finset.antidiagonal m` with `{p \u2208 Finset.antidiagonal (m + fun\u2080 | i => 1) | (fun\u2080 | i => 1) \u2264 p.1}`, exactly the stated subset where `e_i \u2264 a`. Since `Finset.map` is supplied an embedding, the map is injective, and equality with the target subset gives surjectivity, hence the claimed bijection. The binder `[DecidableEq \u03c3]` is required to obtain the finite antidiagonal structure on `\u03c3 \u2192\u2080 \u2115` and is an encoding requirement rather than a mathematically substantive added hypothesis."
}