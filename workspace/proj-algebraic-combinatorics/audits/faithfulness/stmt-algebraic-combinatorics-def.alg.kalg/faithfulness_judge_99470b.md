## TARGET FPS.kalg_zero_smul (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {A : Type u_2} [inst_1 : Ring A] [inst_2 : Algebra K A] (a : A), 0 • a = 0

Docstring: A K-algebra is a K-module: 0 annihilates.
Label: def.alg.Kalg (Property 2) 

## TARGET FPS.kalg_add_smul (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {A : Type u_2} [inst_1 : Ring A] [inst_2 : Algebra K A] (u v : K) (a : A),
  (u + v) • a = u • a + v • a

Docstring: A K-algebra is a K-module: scalar multiplication distributes over addition (right).
Label: def.alg.Kalg (Property 2) 

## TARGET FPS.kalg_smul_zero (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {A : Type u_2} [inst_1 : Ring A] [inst_2 : Algebra K A] (u : K), u • 0 = 0

Docstring: A K-algebra is a K-module: scalar multiplication by zero element gives zero.
Label: def.alg.Kalg (Property 2) 

## TARGET FPS.kalg_mul_smul_comm (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {A : Type u_2} [inst_1 : Ring A] [inst_2 : Algebra K A] (c : K) (a b : A),
  c • (a * b) = a * c • b

Docstring: The compatibility property for K-algebras: `λ(ab) = a(λb)`.
This is equation (7.5.2) in the source.
Label: def.alg.Kalg (Property 3) 

## TARGET FPS.kalg_left_distrib (theorem) — ELABORATED SIGNATURE
∀ {A : Type u_2} [inst : Ring A] (a b c : A), a * (b + c) = a * b + a * c

Docstring: A K-algebra is a ring: left distributivity.
Label: def.alg.Kalg (Property 1) 

## TARGET FPS.kalg_smul_assoc (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {A : Type u_2} [inst_1 : Ring A] [inst_2 : Algebra K A] (u v : K) (a : A),
  u • v • a = (u * v) • a

Docstring: A K-algebra is a K-module: scalar multiplication is associative.
Label: def.alg.Kalg (Property 2) 

## TARGET FPS.kalg_one_mul (theorem) — ELABORATED SIGNATURE
∀ {A : Type u_2} [inst : Ring A] (a : A), 1 * a = a

Docstring: A K-algebra is a ring: one is the multiplicative identity (left).
Label: def.alg.Kalg (Property 1) 

## TARGET FPS.kalg_add_comm (theorem) — ELABORATED SIGNATURE
∀ {A : Type u_2} [inst : Ring A] (a b : A), a + b = b + a

Docstring: A K-algebra is a ring: addition is commutative.
Label: def.alg.Kalg (Property 1) 

## TARGET FPS.kalg_add_assoc (theorem) — ELABORATED SIGNATURE
∀ {A : Type u_2} [inst : Ring A] (a b c : A), a + (b + c) = a + b + c

Docstring: A K-algebra is a ring: addition is associative.
Label: def.alg.Kalg (Property 1) 

## TARGET FPS.kalg_smul_mul_assoc (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {A : Type u_2} [inst_1 : Ring A] [inst_2 : Algebra K A] (c : K) (a b : A),
  c • (a * b) = c • a * b

Docstring: The compatibility property for K-algebras: `λ(ab) = (λa)b`.
This is equation (7.5.2) in the source.
Label: def.alg.Kalg (Property 3) 

## TARGET FPS.kalg_one_smul (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {A : Type u_2} [inst_1 : Ring A] [inst_2 : Algebra K A] (a : A), 1 • a = a

Docstring: A K-algebra is a K-module: 1 acts as identity.
Label: def.alg.Kalg (Property 2) 

## TARGET FPS.kalg_mul_assoc (theorem) — ELABORATED SIGNATURE
∀ {A : Type u_2} [inst : Ring A] (a b c : A), a * (b * c) = a * b * c

Docstring: A K-algebra is a ring: multiplication is associative.
Label: def.alg.Kalg (Property 1) 

## TARGET FPS.kalg_smul_mul_eq_mul_smul (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {A : Type u_2} [inst_1 : Ring A] [inst_2 : Algebra K A] (c : K) (a b : A),
  c • a * b = a * c • b

Docstring: Combined compatibility: `(λa)b = a(λb)`.
Follows from the two parts of equation (7.5.2).
Label: def.alg.Kalg (Property 3) 

## TARGET FPS.kalg_mul_one (theorem) — ELABORATED SIGNATURE
∀ {A : Type u_2} [inst : Ring A] (a : A), a * 1 = a

Docstring: A K-algebra is a ring: one is the multiplicative identity.
Label: def.alg.Kalg (Property 1) 

## TARGET FPS.kalg_smul_add (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {A : Type u_2} [inst_1 : Ring A] [inst_2 : Algebra K A] (u : K) (a b : A),
  u • (a + b) = u • a + u • b

Docstring: A K-algebra is a K-module: scalar multiplication distributes over addition (left).
Label: def.alg.Kalg (Property 2) 

## TARGET FPS.kalg_right_distrib (theorem) — ELABORATED SIGNATURE
∀ {A : Type u_2} [inst : Ring A] (a b c : A), (a + b) * c = a * c + b * c

Docstring: A K-algebra is a ring: right distributivity.
Label: def.alg.Kalg (Property 1) 

## TARGET FPS.kalg_add_zero (theorem) — ELABORATED SIGNATURE
∀ {A : Type u_2} [inst : Ring A] (a : A), a + 0 = a

Docstring: A K-algebra is a ring: zero is the additive identity.
Label: def.alg.Kalg (Property 1) 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Ring
Type u → Type u

Docstring: A `Ring` is a `Semiring` with negation making it an additive group. 

## BASE-LIBRARY REF Algebra
(R : Type u) → (A : Type v) → [CommSemiring R] → [Semiring A] → Type (max u v)

Docstring: An associative unital `R`-algebra is a semiring `A` equipped with a map into its center `R → A`.

See the implementation notes in this file for discussion of the details of this definition.


## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

## BASE-LIBRARY REF Ring.toSemiring
{R : Type u} → [self : Ring R] → Semiring R

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

## BASE-LIBRARY REF Algebra.toSMul
{R : Type u} → {A : Type v} → {inst : CommSemiring R} → {inst_1 : Semiring A} → [self : Algebra R A] → SMul R A

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toMulZeroClass
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → MulZeroClass α

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF NonAssocRing.toNonUnitalNonAssocRing
{α : Type u_1} → [self : NonAssocRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF Ring.toNonAssocRing
{α : Type u} → [Ring α] → NonAssocRing α

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

## INFORMAL STATEMENT
def.alg.Kalg

A $K$\emph{-algebra} is a set $A$ equipped with four maps

\begin{align*}  \oplus &  :A\times A\rightarrow A,\\ \ominus &  :A\times A\rightarrow A,\\ \odot &  :A\times A\rightarrow A,\\ \rightharpoonup &  :K\times A\rightarrow A \end{align*}

 and two elements $\overrightarrow {0}\in A$ and $\overrightarrow {1}\in A$ satisfying the following properties: 

\begin{enumerate} \item The set $A$, equipped with the maps $\oplus $, $\ominus $ and $\odot $ and the two elements $\overrightarrow {0}$ and $\overrightarrow {1}$, is a (noncommutative) ring. 

\item The set $A$, equipped with the maps $\oplus $, $\ominus $ and $\rightharpoonup $ and the element $\overrightarrow {0}$, is a $K$-module. 

\item We have

\begin{equation}  \lambda \rightharpoonup \left( a\odot b\right) =\left( \lambda \rightharpoonup a\right) \odot b=a\odot \left( \lambda \rightharpoonup b\right) \end{equation}

 for all $\lambda \in K$ and $a,b\in A$. 

\end{enumerate}

(Thus, in a nutshell, a $K$-algebra is a set $A$ that is simultaneously a ring and a $K$-module, with the property that the ring $A$ and the $K$-module $A$ have the same addition, the same subtraction and the same zero, and satisfy the additional compatibility property (\ref{eq.def.alg.Kalg.scaleinv}).)

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.alg.module
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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.alg.ring
def.alg.ring

The notion of a \emph{ring} (also known as a \emph{noncommutative ring}) is defined in the exact same way as we defined the notion of a commutative ring in Definition~ \ref{def.alg.commring}, except that the “Commutativity of multiplication” axiom is removed.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The algebra-specific declarations quantify over exactly the intended setting: `\u2200 {K} [CommRing K] {A} [Ring A] [Algebra K A]`. This matches \u201cLet K be a commutative ring\u201d and the blueprint\u2019s characterization of a K-algebra as simultaneously a ring and K-module with compatible multiplication. The library definition of `Algebra K A` is an associative unital algebra whose scalar map lands in the center, which yields precisely the blueprint compatibility `\u03bb \u2022 (a*b) = (\u03bb\u2022a)*b = a*(\u03bb\u2022b)`, represented by `kalg_smul_mul_assoc`, `kalg_mul_smul_comm`, and `kalg_smul_mul_eq_mul_smul`. The module targets exactly reproduce the listed axioms, including `u \u2022 v \u2022 a = (u*v) \u2022 a`, distributivity, identity, and both annihilation laws. The ring targets exactly reproduce the corresponding ring axioms. Those ring targets assume only `\u2200 {A} [Ring A]`, omitting K and the algebra structure; this is a harmless strict generalization, since the conclusions depend only on Property 1. The shared Ring and Algebra structures also ensure that the ring and module operations have the same addition and zero, as required by the blueprint."
}