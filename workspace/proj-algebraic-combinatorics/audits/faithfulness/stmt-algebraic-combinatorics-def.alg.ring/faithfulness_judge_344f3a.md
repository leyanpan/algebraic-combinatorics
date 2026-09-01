## TARGET FPS.ring_mul_zero (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a : R), a * 0 = 0

Docstring: **Annihilation** (Ring property):
`a * 0 = 0` for all `a ∈ R`. 

## TARGET FPS.ring_zero_add (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a : R), 0 + a = a

Docstring: **Neutrality of zero** (Ring axiom):
`0 + a = a` for all `a ∈ R`. 

## TARGET FPS.ring_add_assoc (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a b c : R), a + (b + c) = a + b + c

Docstring: **Associativity of addition** (Ring axiom):
`a + (b + c) = (a + b) + c` for all `a, b, c ∈ R`. 

## TARGET FPS.ring_mul_one (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a : R), a * 1 = a

Docstring: **Neutrality of one** (Ring axiom):
`a * 1 = a` for all `a ∈ R`. 

## TARGET FPS.ring_add_zero (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a : R), a + 0 = a

Docstring: **Neutrality of zero** (Ring axiom):
`a + 0 = a` for all `a ∈ R`. 

## TARGET FPS.ring_mul_assoc (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a b c : R), a * (b * c) = a * b * c

Docstring: **Associativity of multiplication** (Ring axiom):
`a * (b * c) = (a * b) * c` for all `a, b, c ∈ R`. 

## TARGET FPS.ring_right_distrib (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a b c : R), (a + b) * c = a * c + b * c

Docstring: **Right distributivity** (Ring axiom):
`(a + b) * c = a * c + b * c` for all `a, b, c ∈ R`. 

## TARGET FPS.ring_one_mul (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a : R), 1 * a = a

Docstring: **Neutrality of one** (Ring axiom):
`1 * a = a` for all `a ∈ R`. 

## TARGET FPS.ring_add_neg (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a : R), a + -a = 0

Docstring: **Existence of additive inverse** (Ring axiom):
`a + (-a) = 0` for all `a ∈ R`. 

## TARGET FPS.ring_left_distrib (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a b c : R), a * (b + c) = a * b + a * c

Docstring: **Left distributivity** (Ring axiom):
`a * (b + c) = a * b + a * c` for all `a, b, c ∈ R`. 

## TARGET FPS.ring_zero_mul (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a : R), 0 * a = 0

Docstring: **Annihilation** (Ring property):
`0 * a = 0` for all `a ∈ R`. 

## TARGET FPS.ring_add_comm (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : Ring R] (a b : R), a + b = b + a

Docstring: **Commutativity of addition** (Ring axiom):
`a + b = b + a` for all `a, b ∈ R`.
Note: Addition is always commutative, even in noncommutative rings. 

## BASE-LIBRARY REF Ring
Type u → Type u

Docstring: A `Ring` is a `Semiring` with negation making it an additive group. 

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

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toDistrib
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → Distrib α

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF NonAssocRing.toNonUnitalNonAssocRing
{α : Type u_1} → [self : NonAssocRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF Ring.toNonAssocRing
{α : Type u} → [Ring α] → NonAssocRing α

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

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF AddMonoidWithOne.toOne
{R : Type u_2} → [self : AddMonoidWithOne R] → One R

## BASE-LIBRARY REF AddGroupWithOne.toAddMonoidWithOne
{R : Type u} → [self : AddGroupWithOne R] → AddMonoidWithOne R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF NegZeroClass.toNeg
{G : Type u_2} → [self : NegZeroClass G] → Neg G

## BASE-LIBRARY REF SubNegZeroMonoid.toNegZeroClass
{G : Type u_2} → [self : SubNegZeroMonoid G] → NegZeroClass G

## BASE-LIBRARY REF SubtractionMonoid.toSubNegZeroMonoid
{α : Type u_1} → [SubtractionMonoid α] → SubNegZeroMonoid α

## BASE-LIBRARY REF SubtractionCommMonoid.toSubtractionMonoid
{G : Type u} → [self : SubtractionCommMonoid G] → SubtractionMonoid G

## BASE-LIBRARY REF AddCommGroup.toDivisionAddCommMonoid
{G : Type u_1} → [AddCommGroup G] → SubtractionCommMonoid G

## BASE-LIBRARY REF LieRing.toAddCommGroup
{L : Type v} → [self : LieRing L] → AddCommGroup L

## BASE-LIBRARY REF LieRing.ofAssociativeRing
{A : Type v} → [Ring A] → LieRing A

Docstring: An associative ring gives rise to a Lie ring by taking the bracket to be the ring commutator. 

## INFORMAL STATEMENT
def.alg.ring

The notion of a \emph{ring} (also known as a \emph{noncommutative ring}) is defined in the exact same way as we defined the notion of a commutative ring in Definition~ \ref{def.alg.commring}, except that the “Commutativity of multiplication” axiom is removed.

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

## VERDICT
{
  "verdict": "drift",
  "justification": "The discrepancy enters through `FPS.ring_add_neg`, whose elaborated statement is only `\u2200 {R} [Ring R] (a : R), a + -a = 0`. The blueprint instead equips the ring with a binary subtraction map and requires, for all three elements, \u201c`a \u2295 b = c` if and only if `a = c \u2296 b`.\u201d Thus the formal declaration replaces a universally quantified biconditional about binary subtraction (`a`, `b`, and `c`) with an equation about unary negation (`a` only), and none of the other targets states how the blueprint\u2019s binary subtraction is represented. The remaining targets match the other axioms, with two-sided laws appropriately split into separate declarations. To make the package faithful, add or replace this declaration with a theorem of the form `\u2200 (a b c : R), a + b = c \u2194 a = c - b`; alternatively, explicitly define the blueprint subtraction by `c \u2296 b := c + (-b)` and state/prove the corresponding biconditional."
}