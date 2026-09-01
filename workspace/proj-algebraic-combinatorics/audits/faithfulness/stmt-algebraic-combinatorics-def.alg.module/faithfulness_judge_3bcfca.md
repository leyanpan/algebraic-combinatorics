## TARGET AlgebraicCombinatorics.FPS.module_one_smul (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {M : Type u_2} [inst_1 : AddCommGroup M] [inst_2 : _root_.Module K M] (a : M),
  1 • a = a

Docstring: **Neutrality of one** (Axiom 8 in def.alg.module):
`1 • a = a` for all `a ∈ M`. 

## TARGET AlgebraicCombinatorics.FPS.module_smul_zero (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {M : Type u_2} [inst_1 : AddCommGroup M] [inst_2 : _root_.Module K M] (u : K),
  u • 0 = 0

Docstring: **Right annihilation** (Axiom 10 in def.alg.module):
`u • 0 = 0` for all `u ∈ K`. 

## TARGET AlgebraicCombinatorics.FPS.module_add_smul (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {M : Type u_2} [inst_1 : AddCommGroup M] [inst_2 : _root_.Module K M] (u v : K)
  (a : M), (u + v) • a = u • a + v • a

Docstring: **Right distributivity** (Axiom 7 in def.alg.module):
`(u + v) • a = u • a + v • a` for all `u, v ∈ K` and `a ∈ M`. 

## TARGET AlgebraicCombinatorics.FPS.module_smul_add (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {M : Type u_2} [inst_1 : AddCommGroup M] [inst_2 : _root_.Module K M] (u : K)
  (a b : M), u • (a + b) = u • a + u • b

Docstring: **Left distributivity** (Axiom 6 in def.alg.module):
`u • (a + b) = u • a + u • b` for all `u ∈ K` and `a, b ∈ M`. 

## TARGET AlgebraicCombinatorics.FPS.module_add_zero (theorem) — ELABORATED SIGNATURE
∀ {M : Type u_2} [inst : AddCommGroup M] (a : M), a + 0 = a

Docstring: **Neutrality of zero** (Axiom 3 in def.alg.module):
`a + 0 = a` for all `a ∈ M`. 

## TARGET AlgebraicCombinatorics.FPS.module_smul_assoc (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {M : Type u_2} [inst_1 : AddCommGroup M] [inst_2 : _root_.Module K M] (u v : K)
  (a : M), u • v • a = (u * v) • a

Docstring: **Associativity of scaling** (Axiom 5 in def.alg.module):
`u • (v • a) = (u * v) • a` for all `u, v ∈ K` and `a ∈ M`. 

## TARGET AlgebraicCombinatorics.FPS.module_add_assoc (theorem) — ELABORATED SIGNATURE
∀ {M : Type u_2} [inst : AddCommGroup M] (a b c : M), a + (b + c) = a + b + c

Docstring: **Associativity of addition** (Axiom 2 in def.alg.module):
`a + (b + c) = (a + b) + c` for all `a, b, c ∈ M`. 

## TARGET AlgebraicCombinatorics.FPS.module_add_comm (theorem) — ELABORATED SIGNATURE
∀ {M : Type u_2} [inst : AddCommGroup M] (a b : M), a + b = b + a

Docstring: **Commutativity of addition** (Axiom 1 in def.alg.module):
`a + b = b + a` for all `a, b ∈ M`. 

## TARGET AlgebraicCombinatorics.FPS.module_sub_iff_add (theorem) — ELABORATED SIGNATURE
∀ {M : Type u_2} [inst : AddCommGroup M] (a b c : M), a + b = c ↔ a = c - b

Docstring: **Subtraction undoes addition** (Axiom 4 in def.alg.module):
`a + b = c ↔ a = c - b` for all `a, b, c ∈ M`. 

## TARGET AlgebraicCombinatorics.FPS.module_zero_smul (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {M : Type u_2} [inst_1 : AddCommGroup M] [inst_2 : _root_.Module K M] (a : M),
  0 • a = 0

Docstring: **Left annihilation** (Axiom 9 in def.alg.module):
`0 • a = 0` for all `a ∈ M`. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF AddCommGroup
Type u → Type u

Docstring: An additive commutative group is an additive group with commutative `(+)`. 

## BASE-LIBRARY REF Module
(R : Type u) → (M : Type v) → [Semiring R] → [AddCommMonoid M] → Type (max u v)

Docstring: A module is a generalization of vector spaces to a scalar semiring.
It consists of a scalar semiring `R` and an additive monoid of "vectors" `M`,
connected by a "scalar multiplication" operation `r • x : M`
(where `r : R` and `x : M`) with some natural associativity and
distributivity axioms similar to those on a ring. 

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

## BASE-LIBRARY REF AddCommGroup.toAddCommMonoid
{G : Type u} → [self : AddCommGroup G] → AddCommMonoid G

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

## BASE-LIBRARY REF HSMul.hSMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSMul α β γ] → α → β → γ

Docstring: `a • b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent, but it is intended to be used for left actions. 

Conventions for notations in identifiers:

 * The recommended spelling of `•` in identifiers is `smul`.

## BASE-LIBRARY REF instHSMul
{α : Type u_1} → {β : Type u_2} → [SMul α β] → HSMul α β β

## BASE-LIBRARY REF SMulZeroClass.toSMul
{M : Type u_12} → {A : Type u_13} → {inst : Zero A} → [self : SMulZeroClass M A] → SMul M A

## BASE-LIBRARY REF AddZero.toZero
{M : Type u_2} → [self : AddZero M] → Zero M

## BASE-LIBRARY REF AddZeroClass.toAddZero
{M : Type u} → [self : AddZeroClass M] → AddZero M

## BASE-LIBRARY REF AddMonoid.toAddZeroClass
{M : Type u} → [self : AddMonoid M] → AddZeroClass M

## BASE-LIBRARY REF SubNegMonoid.toAddMonoid
{G : Type u} → [self : SubNegMonoid G] → AddMonoid G

## BASE-LIBRARY REF AddGroup.toSubNegMonoid
{A : Type u} → [self : AddGroup A] → SubNegMonoid A

## BASE-LIBRARY REF AddCommGroup.toAddGroup
{G : Type u} → [self : AddCommGroup G] → AddGroup G

## BASE-LIBRARY REF DistribSMul.toSMulZeroClass
{M : Type u_12} → {A : Type u_13} → {inst : AddZeroClass A} → [self : DistribSMul M A] → SMulZeroClass M A

## BASE-LIBRARY REF DistribMulAction.toDistribSMul
{M : Type u_1} → {A : Type u_7} → [inst : Monoid M] → [inst_1 : AddMonoid A] → [DistribMulAction M A] → DistribSMul M A

## BASE-LIBRARY REF MonoidWithZero.toMonoid
{M₀ : Type u} → [self : MonoidWithZero M₀] → Monoid M₀

## BASE-LIBRARY REF Semiring.toMonoidWithZero
{α : Type u} → [self : Semiring α] → MonoidWithZero α

## BASE-LIBRARY REF Module.toDistribMulAction
{R : Type u} →
  {M : Type v} → {inst : Semiring R} → {inst_1 : AddCommMonoid M} → [self : _root_.Module R M] → DistribMulAction R M

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF AddMonoidWithOne.toOne
{R : Type u_2} → [self : AddMonoidWithOne R] → One R

## BASE-LIBRARY REF AddGroupWithOne.toAddMonoidWithOne
{R : Type u} → [self : AddGroupWithOne R] → AddMonoidWithOne R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF CommRing.toRing
{α : Type u} → [self : CommRing α] → Ring α

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF NegZeroClass.toZero
{G : Type u_2} → [self : NegZeroClass G] → Zero G

## BASE-LIBRARY REF SubNegZeroMonoid.toNegZeroClass
{G : Type u_2} → [self : SubNegZeroMonoid G] → NegZeroClass G

## BASE-LIBRARY REF SubtractionMonoid.toSubNegZeroMonoid
{α : Type u_1} → [SubtractionMonoid α] → SubNegZeroMonoid α

## BASE-LIBRARY REF SubtractionCommMonoid.toSubtractionMonoid
{G : Type u} → [self : SubtractionCommMonoid G] → SubtractionMonoid G

## BASE-LIBRARY REF AddCommGroup.toDivisionAddCommMonoid
{G : Type u_1} → [AddCommGroup G] → SubtractionCommMonoid G

## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF Distrib.toAdd
{R : Type u_1} → [self : Distrib R] → Add R

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toDistrib
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → Distrib α

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF AddCommMagma.toAdd
{G : Type u} → [self : AddCommMagma G] → Add G

## BASE-LIBRARY REF AddCommSemigroup.toAddCommMagma
{G : Type u} → [self : AddCommSemigroup G] → AddCommMagma G

## BASE-LIBRARY REF AddCommMonoid.toAddCommSemigroup
{M : Type u} → [self : AddCommMonoid M] → AddCommSemigroup M

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

## BASE-LIBRARY REF Iff
Prop → Prop → Prop

Docstring: If and only if, or logical bi-implication. `a ↔ b` means that `a` implies `b` and vice versa.
By `propext`, this implies that `a` and `b` are equal and hence any expression involving `a`
is equivalent to the corresponding expression with `b` instead.


Conventions for notations in identifiers:

 * The recommended spelling of `↔` in identifiers is `iff`.

 * The recommended spelling of `<->` in identifiers is `iff` (prefer `↔` over `<->`).

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

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toMulZeroClass
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → MulZeroClass α

## INFORMAL STATEMENT
def.alg.module

Let $K$ be a commutative ring. 

A $K$\emph{-module} means a set $M$ equipped with three maps 

\begin{align*}  \oplus &  :M\times M\rightarrow M,\\ \ominus &  :M\times M\rightarrow M,\\ \rightharpoonup &  :K\times M\rightarrow M \end{align*}

 (notice that the third map has domain $K\times M$, not $M\times M$) and an element $\overrightarrow {0}\in M$ satisfying the following axioms: 

\begin{enumerate} \item \emph{Commutativity of addition:} We have $a\oplus b=b\oplus a$ for all $a,b\in M$. 

\item \emph{Associativity of addition:} We have $a\oplus \left( b\oplus c\right) =\left( a\oplus b\right) \oplus c$ for all $a,b,c\in M$. 

\item \emph{Neutrality of zero:} We have $a\oplus \overrightarrow {0}=\overrightarrow {0}\oplus a=a$ for all $a\in M$. 

\item \emph{Subtraction undoes addition:} Let $a,b,c\in M$. We have $a\oplus b=c$ if and only if $a=c\ominus b$. 

\item \emph{Associativity of scaling:} We have $u\rightharpoonup \left( v\rightharpoonup a\right) =\left( uv\right) \rightharpoonup a$ for all $u,v\in K$ and $a\in M$. 

\item \emph{Left distributivity:} We have $u\rightharpoonup \left( a\oplus b\right) =\left( u\rightharpoonup a\right) \oplus \left( u\rightharpoonup b\right) $ for all $u\in K$ and $a,b\in M$. 

\item \emph{Right distributivity:} We have $\left( u+v\right) \rightharpoonup a=\left( u\rightharpoonup a\right) \oplus \left( v\rightharpoonup a\right) $ for all $u,v\in K$ and $a\in M$. 

\item \emph{Neutrality of one:} We have $1\rightharpoonup a=a$ for all $a\in M$. 

\item \emph{Left annihilation:} We have $0\rightharpoonup a=\overrightarrow {0}$ for all $a\in M$. 

\item \emph{Right annihilation:} We have $u\rightharpoonup \overrightarrow {0}=\overrightarrow {0}$ for all $u\in K$. 

\end{enumerate}

The operations $\oplus $, $\ominus $ and $\rightharpoonup $ are called the \emph{addition}, the \emph{subtraction} and the \emph{scaling} (or the $K$\emph{-action}) of the $K$-module $M$. When confusion is unlikely, we will denote these three operations $\oplus $, $\ominus $ and $\rightharpoonup $ by $+$, $-$ and $\cdot $, respectively, and we will abbreviate $a\rightharpoonup b=a\cdot b$ by $ab$. 

The element $\overrightarrow {0}$ is called the \emph{zero} (or the \emph{zero vector}) of the $K$-module $M$. We will usually just call it $0$. 

When $M$ is a $K$-module, the elements of $M$ are called \emph{vectors}, while the elements of $K$ are called \emph{scalars}. 

We will use \emph{PEMDAS conventions} for the three operations $\oplus $, $\ominus $ and $\rightharpoonup $, with the operation $\rightharpoonup $ having higher precedence than $\oplus $ and $\ominus $.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal binders ` [CommRing K]`, `[AddCommGroup M]`, and `[_root_.Module K M]` faithfully encode the blueprint setting \u201cLet K be a commutative ring\u201d and a K-module with additive group operations and scalar action. The conclusions match the ten listed axioms: for example, `u \u2022 v \u2022 a = (u * v) \u2022 a`, `u \u2022 (a + b) = u \u2022 a + u \u2022 b`, `(u + v) \u2022 a = u \u2022 a + v \u2022 a`, and `a + b = c \u2194 a = c - b` directly correspond to axioms 5, 6, 7, and 4. Likewise, the one- and zero-scaling laws match axioms 8\u201310. For axiom 3, `module_add_zero` states only `a + 0 = a`, whereas the blueprint writes `a \u2295 0 = 0 \u2295 a = a`; however, the other side follows from `module_add_comm` (and is also part of the `AddCommGroup` setting), so the package implies the full blueprint axiom. Using `Type` rather than \u201cset\u201d is harmlessly more general, and the apparently stronger `AddCommGroup` hypothesis is not an added mathematical restriction because the blueprint\u2019s addition, zero, and subtraction-undoes-addition axioms give precisely the corresponding additive-group structure."
}