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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF Equiv.Perm.instOne
{α : Type u_4} → One (Equiv.Perm α)

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

## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF Equiv.trans
{α : Sort u} → {β : Sort v} → {γ : Sort w} → α ≃ β → β ≃ γ → α ≃ γ

Docstring: Composition of equivalences `e₁ : α ≃ β` and `e₂ : β ≃ γ`. 

## BASE-LIBRARY REF Equiv.symm
{α : Sort u} → {β : Sort v} → α ≃ β → β ≃ α

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
  "verdict": "unclear",
  "justification": "The conjugation theorem faithfully strengthens part (a): its binders `(\u03c3 : Equiv.Perm \u03b1) (e : \u03b1 \u2243 \u03b2)` and expression `((e.symm.trans \u03c3).trans e)` denote, from the supplied `Equiv.trans`/`Equiv.symm` documentation, the transported permutation `e \u2218 \u03c3 \u2218 e\u207b\u00b9`. Taking `e = \u03c6\u2081` and `e = \u03c6\u2082` gives the stated independence from the bijection, and allowing arbitrary finite `\u03b2` is more general. However, parts (b) and (c) cannot be fully compared because the package gives only the signatures, not the meanings, of `Equiv.Perm.instOne` and `Equiv.Perm.instMul`. Thus it does not establish that the formal `1` in `Equiv.Perm.sign 1 = 1` is the identity map, or that `\u03c3 * \u03c4` in `Equiv.Perm.sign (\u03c3 * \u03c4) = ...` is the blueprint product `\u03c3 \u2218 \u03c4`, which the informal definition explicitly says sends `x` to `\u03c3 (\u03c4 x)`. The generic `HMul.hMul` documentation even says multiplication is type-dependent. The package would need the instance bodies or facts such as `(1 : Equiv.Perm \u03b1) x = x` and `(\u03c3 * \u03c4) x = \u03c3 (\u03c4 x)`. With those standard meanings, all three targets are faithful; the `DecidableEq` binders merely encode what is needed to define the finite-type sign rather than a mathematically substantive restriction."
}