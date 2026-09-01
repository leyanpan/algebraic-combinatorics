## TARGET AlgebraicCombinatorics.SymmetricGroup (def) — ELABORATED SIGNATURE
Type u_1 → Type (max 0 u_1)

Body:
fun X => Equiv.Perm X

Docstring: The symmetric group of a type `X` is the group of all permutations of `X`.
(def.perm.perm (b))

In Mathlib, this is `Equiv.Perm X` with its natural `Group` instance. 

## TARGET AlgebraicCombinatorics.perm_zpow_neg_one (theorem) — ELABORATED SIGNATURE
∀ {X : Type u_1} (α : Equiv.Perm X), α ^ (-1) = α⁻¹

Docstring: `α^(-1)` is the inverse of `α`. (def.perm.perm (d)) 

## TARGET AlgebraicCombinatorics.symmetricGroup_card (theorem) — ELABORATED SIGNATURE
∀ (X : Type u_1) [inst : Fintype X] [inst_1 : DecidableEq X], Fintype.card (Equiv.Perm X) = (Fintype.card X).factorial

Docstring: The symmetric group of a finite type has `|X|!` elements. (def.perm.perm (b)) 

## TARGET AlgebraicCombinatorics.perm_mul_apply (theorem) — ELABORATED SIGNATURE
∀ {X : Type u_1} (α β : Equiv.Perm X) (x : X), (α * β) x = α (β x)

Docstring: The composition `α * β` sends `x` to `α(β(x))`. (def.perm.perm (c)) 

## TARGET AlgebraicCombinatorics.perm_pow_apply (theorem) — ELABORATED SIGNATURE
∀ {X : Type u_1} (α : Equiv.Perm X) (n : ℕ) (x : X), (α ^ n) x = (⇑α)^[n] x

Docstring: Applying `α^n` to `x` gives the n-fold application of `α`. 

## TARGET AlgebraicCombinatorics.Permutation (def) — ELABORATED SIGNATURE
Type u_1 → Type (max 0 u_1)

Body:
fun X => Equiv.Perm X

Docstring: A permutation of a type `X` is a bijection from `X` to itself. (def.perm.perm (a))

In Mathlib, this is `Equiv.Perm X := X ≃ X`, i.e., the type of equivalences from `X` to `X`. 

## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

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

## BASE-LIBRARY REF HPow.hPow
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HPow α β γ] → α → β → γ

Docstring: `a ^ b` computes `a` to the power of `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `^` in identifiers is `pow`.

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF instHPow
{α : Type u_1} → {β : Type u_2} → [Pow α β] → HPow α β α

## BASE-LIBRARY REF DivInvMonoid.toZPow
{M : Type u_2} → [DivInvMonoid M] → Pow M ℤ

## BASE-LIBRARY REF Group.toDivInvMonoid
{G : Type u} → [self : Group G] → DivInvMonoid G

## BASE-LIBRARY REF Equiv.Perm.permGroup
{α : Type u_4} → Group (Equiv.Perm α)

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

## BASE-LIBRARY REF Inv.inv
{α : Type u} → [self : Inv α] → α → α

Docstring: `a⁻¹` computes the inverse of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `⁻¹` in identifiers is `inv`.

## BASE-LIBRARY REF Equiv.Perm.instInv
{α : Type u_4} → Inv (Equiv.Perm α)

## BASE-LIBRARY REF Fintype
Type u_4 → Type u_4

Docstring: `Fintype α` means that `α` is finite, i.e. there are only
finitely many distinct elements of type `α`. The evidence of this
is a finset `elems` (a list up to permutation without duplicates),
together with a proof that everything of type `α` is in the list. 

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Fintype.card
(α : Type u_4) → [Fintype α] → ℕ

Docstring: `card α` is the number of elements in `α`, defined when `α` is a fintype. 

## BASE-LIBRARY REF Equiv.instFintype
{α : Type u_1} → {β : Type u_2} → [DecidableEq α] → [DecidableEq β] → [Fintype α] → [Fintype β] → Fintype (α ≃ β)

## BASE-LIBRARY REF Nat.factorial
ℕ → ℕ

Docstring: `Nat.factorial n` is the factorial of `n`. 

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

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

## BASE-LIBRARY REF Equiv.Perm.instPowNat
{α : Type u_4} → Pow (Equiv.Perm α) ℕ

## BASE-LIBRARY REF Nat.iterate
{α : Sort u} → (α → α) → ℕ → α → α

Docstring: Iterate a function. 

## INFORMAL STATEMENT
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The declarations match the components of the blueprint. `Permutation` and `SymmetricGroup` both have body `fun X => Equiv.Perm X`, while `Equiv.Perm` is documented as \u201cthe type of bijections from `\u03b1` to itself,\u201d matching (a) and the underlying set of the symmetric group in (b); its supplied natural `Group` instance provides the group structure. `symmetricGroup_card` states `Fintype.card (Equiv.Perm X) = (Fintype.card X).factorial`, exactly the claim that its size is `|X|!` when finite. Its extra `[DecidableEq X]` is an implementation/encoding requirement for constructing the relevant `Fintype` instance, not a mathematically substantive restriction. `perm_mul_apply` states `(\u03b1 * \u03b2) x = \u03b1 (\u03b2 x)`, matching the composition convention in (c). Finally, `perm_pow_apply` states that natural powers are iterated application, and `perm_zpow_neg_one` states `\u03b1 ^ (-1) = \u03b1\u207b\u00b9`, matching the corresponding assertions in (d). Quantifying over arbitrary types rather than only a fixed set is a harmless generalization."
}