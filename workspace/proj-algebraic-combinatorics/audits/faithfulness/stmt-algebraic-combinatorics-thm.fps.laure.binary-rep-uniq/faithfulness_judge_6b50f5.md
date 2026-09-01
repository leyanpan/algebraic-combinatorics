## TARGET AlgebraicCombinatorics.FPS.Laurent.binaryRepresentation_exists_unique (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ), ∃! s, AlgebraicCombinatorics.FPS.Laurent.BinaryRepresentation n s

Docstring: **Unique Binary Representation Theorem**.
(Theorem thm.fps.laure.binary-rep-uniq, label: thm.fps.laure.binary-rep-uniq)

Each natural number `n` has a unique binary representation. More precisely, there exists
a unique finset `s ⊆ ℕ` such that `n = ∑_{i ∈ s} 2^i`.

This is a fundamental result that motivates the study of Laurent series: when trying to
prove the analogous result for balanced ternary representations (where coefficients can
be -1, 0, or 1), we need to work with negative powers of the base, which leads naturally
to Laurent series. 

## TARGET AlgebraicCombinatorics.binaryRepresentation_exists (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ), Nonempty (AlgebraicCombinatorics.BinaryRepresentation n)

Docstring: Every natural number has a binary representation.
This is part of Theorem `thm.fps.laure.binary-rep-uniq`. 

## TARGET AlgebraicCombinatorics.binaryRepresentation_unique (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ) (r₁ r₂ : AlgebraicCombinatorics.BinaryRepresentation n), r₁.bits = r₂.bits

Docstring: The binary representation of a natural number is unique.
This is Theorem `thm.fps.laure.binary-rep-uniq`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.BinaryRepresentation (def)
ℕ → Finset ℕ → Prop

Body:
fun n s => n = ∑ i ∈ s, 2 ^ i

Docstring: **Binary Representation Definition**.

A binary representation of `n` is a finset `s ⊆ ℕ` such that `n = ∑_{i ∈ s} 2^i`.
This is equivalent to specifying which bits are 1 in the binary expansion.

The essentially finite sequence `(bᵢ)_{i ∈ ℕ}` from the textbook corresponds to
`bᵢ = 1` if `i ∈ s`, and `bᵢ = 0` otherwise. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.BinaryRepresentation (inductive)
ℕ → Type

Body:
AlgebraicCombinatorics.BinaryRepresentation.mk : {n : ℕ} →
  (bits : ℕ → Fin 2) →
    {i | bits i ≠ 0}.Finite → ∑ᶠ (i : ℕ), ↑(bits i) * 2 ^ i = n → AlgebraicCombinatorics.BinaryRepresentation n

Docstring: A binary representation of a nonnegative integer `n` is an essentially finite
sequence `(b_i)_{i ∈ ℕ}` of elements in `{0, 1}` such that `n = ∑ b_i * 2^i`.

This corresponds to Definition in `sec.gf.laure` of the source.


## PROJECT DEPENDENCY AlgebraicCombinatorics.BinaryRepresentation.bits (def)
{n : ℕ} → AlgebraicCombinatorics.BinaryRepresentation n → ℕ → Fin 2

Body:
fun n self => self.1

Docstring: The sequence of bits 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF ExistsUnique
{α : Sort u_1} → (α → Prop) → Prop

Docstring: For `p : α → Prop`, `ExistsUnique p` means that there exists a unique `x : α` with `p x`. 

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

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

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Nonempty
Sort u → Prop

Docstring: `Nonempty α` is a typeclass that says that `α` is not an empty type,
that is, there exists an element in the type. It differs from `Inhabited α`
in that `Nonempty α` is a `Prop`, which means that it does not actually carry
an element of `α`, only a proof that *there exists* such an element.
Given `Nonempty α`, you can construct an element of `α` *nonconstructively*
using `Classical.choice`.


## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

## BASE-LIBRARY REF Fin.instOfNat
{n : ℕ} → [NeZero n] → {i : ℕ} → OfNat (Fin n) i

## BASE-LIBRARY REF Nat.instNeZeroSucc
∀ {n : ℕ}, NeZero (n + 1)

## BASE-LIBRARY REF finsum
{M : Type u_7} → {α : Sort u_8} → [AddCommMonoid M] → (α → M) → M

Docstring: Sum of `f x` as `x` ranges over the elements of the support of `f`, if it's finite. Zero
otherwise. 

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF instMulNat
Mul ℕ

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## INFORMAL STATEMENT
thm.fps.laure.binary-rep-uniq

Each $n\in \mathbb {N}$ has a unique binary representation.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.laure.binary-rep
def.fps.laure.binary-rep

\leanhelper  A \emph{binary representation} of an integer $n$ means an essentially finite sequence $\left( b_{i}\right) _{i\in \mathbb {N}}=\left( b_{0},b_{1},b_{2},\ldots \right) \in \left\{  0,1\right\}  ^{\mathbb {N}}$ such that

\[  n=\sum _{i\in \mathbb {N}}b_{i}2^{i}.  \]

 (Recall that “essentially finite” means “all but finitely many $i\in \mathbb {N}$ satisfy $b_{i}=0$”.)

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint says: \u201cEach $n\\in\\mathbb N$ has a unique binary representation,\u201d where a representation is an essentially finite sequence of bits satisfying $n=\\sum_i b_i2^i$. The principal target quantifies exactly over naturals, `\u2200 (n : \u2115)`, and asserts `\u2203! s, ... BinaryRepresentation n s`. Its dependency defines this predicate as `n = \u2211 i \u2208 s, 2 ^ i` for `s : Finset \u2115`. A finite set `s` is equivalently the essentially finite bit sequence with `b_i = 1` exactly when `i \u2208 s`, as the dependency docstring explicitly records, so existence and uniqueness of such a finset are equivalent to existence and uniqueness of the blueprint\u2019s sequence. The auxiliary declarations also match the sequence formulation: `Nonempty (AlgebraicCombinatorics.BinaryRepresentation n)` gives existence, while `r\u2081.bits = r\u2082.bits` gives uniqueness of the underlying bit sequence. Equality of proof fields is not required because the informal representation is the sequence itself."
}