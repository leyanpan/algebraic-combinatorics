## TARGET Equiv.Perm.sign_id_finiteSet (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_1} [inst : DecidableEq α] [inst_1 : Fintype α], Equiv.Perm.sign 1 = 1

Docstring: **Proposition (prop.perm.sign.X)(b)**
The identity permutation of any finite set has sign 1. 

## TARGET Equiv.Perm.sign_mul_finiteSet (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_1} [inst : DecidableEq α] [inst_1 : Fintype α] (σ τ : Equiv.Perm α),
  Equiv.Perm.sign (σ * τ) = Equiv.Perm.sign σ * Equiv.Perm.sign τ

Docstring: **Proposition (prop.perm.sign.X)(c)**
The sign is multiplicative for permutations of any finite set. 

## TARGET Equiv.Perm.sign_conj_eq (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_1} [inst : DecidableEq α] [inst_1 : Fintype α] {β : Type u_2} [inst_2 : DecidableEq β]
  [inst_3 : Fintype β] (σ : Equiv.Perm α) (e : α ≃ β), Equiv.Perm.sign ((e.symm.trans σ).trans e) = Equiv.Perm.sign σ

Docstring: **Proposition (prop.perm.sign.X)(a)**
The sign of a permutation of a finite set is independent of the chosen bijection.

For any bijections φ₁, φ₂ : X → [n], we have sign_{φ₁}(σ) = sign_{φ₂}(σ). 

## BASE-LIBRARY REF Fintype
Type u_4 → Type u_4

Docstring: `Fintype α` means that `α` is finite, i.e. there are only
finitely many distinct elements of type `α`. The evidence of this
is a finset `elems` (a list up to permutation without duplicates),
together with a proof that everything of type `α` is in the list. 

## BASE-LIBRARY REF Units
(α : Type u) → [Monoid α] → Type u

Docstring: Units of a `Monoid`, bundled version. Notation: `αˣ`.

An element of a `Monoid` is a unit if it has a two-sided inverse.
This version bundles the inverse element so that it can be computed.
For a predicate see `IsUnit`. 

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


## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Body:
fun α => α ≃ α

Docstring: `Perm α` is the type of bijections from `α` to itself. 

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

## BASE-LIBRARY REF Equiv.Perm.instMul
{α : Type u_4} → Mul (Equiv.Perm α)

Body:
fun {α} => { mul := fun f g => Equiv.trans g f }

Characterization: `(σ * τ) x = σ (τ x)`: multiplication is composition, right factor first (`Equiv.Perm.coe_mul`).

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

## BASE-LIBRARY REF One
Type u → Type u

Docstring: A type with a "one" element. 

## BASE-LIBRARY REF One.one
{α : Type u} → [self : One α] → α

Body:
fun α [self : One α] => self.1

Docstring: The "one" element of the type. 

## BASE-LIBRARY REF Units.instOne
{α : Type u} → [inst : Monoid α] → One αˣ

Body:
fun {α} [Monoid α] => { one := { val := 1, inv := 1, val_inv := ⋯, inv_val := ⋯ } }

Docstring: Units of a monoid have a unit 

## BASE-LIBRARY REF Mul
Type u → Type u

Docstring: The homogeneous version of `HMul`: `a * b : α` where `a b : α`. 

## BASE-LIBRARY REF Mul.mul
{α : Type u} → [self : Mul α] → α → α → α

Body:
fun α [self : Mul α] => self.1

Docstring: `a * b` computes the product of `a` and `b`. See `HMul`. 

## BASE-LIBRARY REF Units.instMul
{α : Type u} → [inst : Monoid α] → Mul αˣ

Body:
fun {α} [Monoid α] => { mul := fun u₁ u₂ => { val := ↑u₁ * ↑u₂, inv := u₂.inv * u₁.inv, val_inv := ⋯, inv_val := ⋯ } }

Docstring: Units of a monoid have an induced multiplication. 

## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF Equiv.trans
{α : Sort u} → {β : Sort v} → {γ : Sort w} → α ≃ β → β ≃ γ → α ≃ γ

Body:
fun {α} {β} {γ} e₁ e₂ => { toFun := ⇑e₂ ∘ ⇑e₁, invFun := ⇑e₁.symm ∘ ⇑e₂.symm, left_inv := ⋯, right_inv := ⋯ }

Docstring: Composition of equivalences `e₁ : α ≃ β` and `e₂ : β ≃ γ`. 

## BASE-LIBRARY REF Equiv.symm
{α : Sort u} → {β : Sort v} → α ≃ β → β ≃ α

Body:
fun {α} {β} e => { toFun := e.invFun, invFun := e.toFun, left_inv := ⋯, right_inv := ⋯ }

Docstring: Inverse of an equivalence `e : α ≃ β`. 

## INFORMAL STATEMENT
prop.perm.sign.X

Let $X$ be a finite set. We want to define the sign of any permutation of $X$. 

Fix a bijection $\phi : X \to [n]$ for some $n \in \mathbb {N}$. (Such a bijection always exists, since $X$ is finite.) For every permutation $\sigma $ of $X$, set 

\[  (-1)_{\phi }^{\sigma } := (-1)^{\phi \circ \sigma \circ \phi ^{-1}}.  \]

 Here, the right hand side is well-defined, since $\phi \circ \sigma \circ \phi ^{-1}$ is a permutation of $[n]$. Now: 

\textbf{(a)} This number $(-1)_{\phi }^{\sigma }$ depends only on the permutation $\sigma $, but not on the bijection $\phi $. (In other words, if $\phi _1$ and $\phi _2$ are two bijections from $X$ to $[n]$, then $(-1)_{\phi _1}^{\sigma } = (-1)_{\phi _2}^{\sigma }$.) 

Thus, we shall denote $(-1)_{\phi }^{\sigma }$ by $(-1)^{\sigma }$ from now on. We refer to this number $(-1)^{\sigma }$ as the \emph{sign} of the permutation $\sigma \in S_X$. (When $X = [n]$, this notation does not clash with Definition~ \ref{def.perm.sign}, since we can pick the bijection $\phi = \operatorname {id}$ and obtain $(-1)_{\phi }^{\sigma } = (-1)^{\operatorname {id} \circ \sigma \circ \operatorname {id}^{-1}} = (-1)^{\sigma }$.) 

\textbf{(b)} The identity permutation $\operatorname {id} : X \to X$ satisfies $(-1)^{\operatorname {id}} = 1$. 

\textbf{(c)} We have $(-1)^{\sigma \tau } = (-1)^{\sigma } \cdot (-1)^{\tau }$ for any two permutations $\sigma $ and $\tau $ of $X$.

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
  "discrepancies": [],
  "justification": "All three targets certify the corresponding parts of the blueprint. For (a), the formal conjugate `((e.symm.trans \u03c3).trans e)` is exactly `e \u2218 \u03c3 \u2218 e\u207b\u00b9`; thus `Equiv.Perm.sign ((e.symm.trans \u03c3).trans e) = Equiv.Perm.sign \u03c3` applied to each `e = \u03c6\u2081, \u03c6\u2082` gives equality of the two transported signs. For (b), `Equiv.Perm.sign 1 = 1` directly matches \u201cthe identity permutation ... satisfies ... = 1,\u201d since `(1 : Equiv.Perm \u03b1)` is the identity. For (c), `Equiv.Perm.sign (\u03c3 * \u03c4) = Equiv.Perm.sign \u03c3 * Equiv.Perm.sign \u03c4` matches the stated multiplicativity, and permutation multiplication has the blueprint\u2019s convention `(\u03c3 * \u03c4) x = \u03c3 (\u03c4 x)`. The codomain `\u2124\u02e3` merely bundles the integer values `1` and `-1` as units; equality and multiplication there certify the corresponding integer statements. The `DecidableEq` and `Fintype` instances encode the finite Lean setting."
}