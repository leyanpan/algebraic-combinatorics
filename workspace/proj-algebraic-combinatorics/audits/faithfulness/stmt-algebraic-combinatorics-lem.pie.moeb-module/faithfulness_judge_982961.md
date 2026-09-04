## TARGET BooleanMobius.booleanMobiusInversion' (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_1} [inst : DecidableEq α] {S : Finset α} {A : Type u_2} [inst_1 : AddCommGroup A] [_root_.Module ℤ A]
  (a b : Finset α → A),
  (∀ I ⊆ S, b I = ∑ J ∈ I.powerset, a J) → ∀ I ⊆ S, a I = ∑ J ∈ I.powerset, (-1) ^ (I \ J).card • b J

Docstring: Alternative formulation of Boolean Möbius inversion using (-1)^|I \ J| as an integer.
This is sometimes more convenient for computation. 

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

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

## BASE-LIBRARY REF Int.instSemiring
Semiring ℤ

Body:
inferInstance

## BASE-LIBRARY REF Semiring
Type u → Type u

Docstring: A `Semiring` is a type with addition, multiplication, a `0` and a `1` where addition is
commutative and associative, multiplication is associative and left and right distributive over
addition, and `0` and `1` are additive and multiplicative identities. 

## BASE-LIBRARY REF Int.instCommSemiring
CommSemiring ℤ

Body:
inferInstance

## BASE-LIBRARY REF AddCommGroup.add_comm
∀ {G : Type u} [self : AddCommGroup G] (a b : G), a + b = b + a

Docstring: Addition is commutative in a commutative additive magma. 

## BASE-LIBRARY REF HasSubset.Subset
{α : Type u} → [self : HasSubset α] → α → α → Prop

Body:
fun α [self : HasSubset α] => self.1

Docstring: Subset relation: `a ⊆ b`  

Conventions for notations in identifiers:

 * The recommended spelling of `⊆` in identifiers is `subset`.

## BASE-LIBRARY REF Finset.instHasSubset
{α : Type u_1} → HasSubset (Finset α)

Body:
fun {α} => { Subset := fun s t => ∀ ⦃a : α⦄, a ∈ s → a ∈ t }

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Body:
fun {ι} {M} [AddCommMonoid M] s f => (Multiset.map f s.val).sum

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Finset.powerset
{α : Type u_1} → Finset α → Finset (Finset α)

Body:
fun {α} s => { val := Multiset.pmap Finset.mk s.val.powerset ⋯, nodup := ⋯ }

Docstring: When `s` is a finset, `s.powerset` is the finset of all subsets of `s` (seen as finsets). 

## BASE-LIBRARY REF SMul
Type u → Type v → Type (max u v)

Docstring: Typeclass for types with a scalar multiplication operation, denoted `•` (`\bu`) 

## BASE-LIBRARY REF SMul.smul
{M : Type u} → {α : Type v} → [self : SMul M α] → M → α → α

Body:
fun M α [self : SMul M α] => self.1

Docstring: `m • a : α` denotes the product of `m : M` and `a : α`. The meaning of this notation is type-dependent,
but it is intended to be used for left actions. 

## BASE-LIBRARY REF SubNegMonoid
Type u → Type u

Docstring: A `SubNegMonoid` is an `AddMonoid` with unary `-` and binary `-` operations
satisfying `sub_eq_add_neg : ∀ a b, a - b = a + -b`.

The default for `sub` is such that `a - b = a + -b` holds by definition.

Adding `sub` as a field rather than defining `a - b := a + -b` allows us to
avoid certain classes of unification failures, for example:
Let `foo X` be a type with a `∀ X, Sub (Foo X)` instance but no
`∀ X, Neg (Foo X)`. Suppose we also have an instance
`∀ X [Cromulent X], AddGroup (Foo X)`. Then the `(-)` coming from
`AddGroup.sub` cannot be definitionally equal to the `(-)` coming from
`Foo.Sub`.

In the same way, adding a `zsmul` field makes it possible to avoid definitional failures
in diamonds. See the definition of `AddMonoid` and Note [forgetful inheritance] for more
explanations on this.


## BASE-LIBRARY REF Pow
Type u → Type v → Type (max u v)

Docstring: The homogeneous version of `HPow`: `a ^ b : α` where `a : α`, `b : β`.
(The right argument is not the same as the left since we often want this even
in the homogeneous case.)

Types can choose to subscribe to particular defaulting behavior by providing
an instance to either `NatPow` or `HomogeneousPow`:
- `NatPow` is for types whose exponents is preferentially a `Nat`.
- `HomogeneousPow` is for types whose base and exponent are preferentially the same.


## BASE-LIBRARY REF Pow.pow
{α : Type u} → {β : Type v} → [self : Pow α β] → α → β → α

Body:
fun α β [self : Pow α β] => self.1

Docstring: `a ^ b` computes `a` to the power of `b`. See `HPow`. 

## BASE-LIBRARY REF Monoid
Type u → Type u

Docstring: A `Monoid` is a `Semigroup` with an element `1` such that `1 * a = a * 1 = a`. 

## BASE-LIBRARY REF Int.instMonoid
Monoid ℤ

Body:
inferInstance

## BASE-LIBRARY REF Int.instCommMonoid
CommMonoid ℤ

Body:
{ toMul := Int.instMul, mul_assoc := Int.mul_assoc, toOne := One.ofOfNat1, one_mul := Int.one_mul,
  mul_one := Int.mul_one, npow := fun n x => x ^ n, npow_zero := ⋯, npow_succ := ⋯, mul_comm := Int.mul_comm }

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Body:
fun α [self : Neg α] => self.1

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF Int.instNegInt
Neg ℤ

Body:
{ neg := Int.neg }

## BASE-LIBRARY REF Int.neg
ℤ → ℤ

Body:
fun n =>
  match n with
  | Int.ofNat n => Int.negOfNat n
  | Int.negSucc n => ↑n.succ

Docstring: Negation of integers, usually accessed via the `-` prefix operator.

This function is overridden by the compiler with an efficient implementation. This definition is
the logical model.

Examples:
 * `-(6 : Int) = -6`
 * `-(-6 : Int) = 6`
 * `(12 : Int).neg = -12`


## BASE-LIBRARY REF Int.ofNat
ℕ → ℤ

Docstring: A natural number is an integer.

This constructor covers the non-negative integers (from `0` to `∞`).


## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Body:
fun {α} s => s.val.card

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF SDiff.sdiff
{α : Type u} → [self : SDiff α] → α → α → α

Body:
fun α [self : SDiff α] => self.1

Docstring: `a \ b` is the set difference of `a` and `b`,
consisting of all elements in `a` that are not in `b`.


Conventions for notations in identifiers:

 * The recommended spelling of `\` in identifiers is `sdiff`.

## BASE-LIBRARY REF Finset.instSDiff
{α : Type u_1} → [DecidableEq α] → SDiff (Finset α)

Body:
fun {α} [DecidableEq α] => { sdiff := fun s₁ s₂ => { val := s₁.val - s₂.val, nodup := ⋯ } }

Docstring: `s \ t` is the set consisting of the elements of `s` that are not in `t`. 

## INFORMAL STATEMENT
lem.pie.moeb-module

\leanhelper  Alternative formulation of Boolean M\"{o}bius inversion (Theorem~ \ref{thm.pie.moeb}) using the $\mathbb {Z}$-module scalar multiplication: under the same hypotheses, for all $I\subseteq S$, 

\[  a_{I}=\sum _{J\subseteq I}\left(-1\right)^{\left\vert I\setminus J\right\vert }\cdot b_{J},  \]

 where the multiplication $(-1)^{|I\setminus J|}\cdot b_J$ denotes the $\mathbb {Z}$-module scalar action.

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

## INFORMAL CONTEXT stmt-algebraic-combinatorics-thm.pie.moeb
Boolean Möbius inversion

Let $S$ be a finite set. Let $A$ be any additive abelian group. 

For each subset $I$ of $S$, let $a_{I}$ and $b_{I}$ be two elements of $A$. 

Assume that 

\begin{equation}  b_{I}=\sum _{J\subseteq I}a_{J}\  \  \  \  \  \  \  \  \  \  \text{for all }I\subseteq S.  \end{equation}

Then, we also have 

\begin{equation}  a_{I}=\sum _{J\subseteq I}\left( -1\right) ^{\left\vert I\setminus J\right\vert }b_{J}\  \  \  \  \  \  \  \  \  \  \text{for all }I\subseteq S.  \end{equation}

## VERDICT
{
  "verdict": "faithful",
  "discrepancies": [],
  "justification": "The formal hypothesis `(\u2200 I \u2286 S, b I = \u2211 J \u2208 I.powerset, a J)` exactly represents the blueprint assumption `b_I = \u2211_{J\u2286I} a_J` for every `I\u2286S`, since `I.powerset` is the finset of all subsets of `I`. Its conclusion `\u2200 I \u2286 S, a I = \u2211 J \u2208 I.powerset, (-1) ^ (I \\ J).card \u2022 b J` exactly represents `a_I = \u2211_{J\u2286I} (-1)^{|I\\setminus J|}\u00b7b_J`, with the coefficient computed in `\u2124` and `\u2022` supplied by `Module \u2124 A`. The binders `[AddCommGroup A] [Module \u2124 A]` match the additive abelian group and integer-module setting. `Finset`, `[DecidableEq \u03b1]`, and defining `a b` on all finsets rather than only subsets of `S` are routine finite-set encodings and do not weaken the claimed result."
}