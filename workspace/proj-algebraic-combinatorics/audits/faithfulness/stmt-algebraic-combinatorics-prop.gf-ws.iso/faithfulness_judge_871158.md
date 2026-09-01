## TARGET WeightedSet.weightGenFun_eq_of_isomorphic (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommSemiring R] {α : Type u_2} {β : Type u_3} (W₁ : WeightedSet α) (W₂ : WeightedSet β)
  (hft₁ : W₁.IsFiniteType) (hft₂ : W₂.IsFiniteType), (W₁ ≅ᵥ W₂) → W₁.weightGenFun hft₁ = W₂.weightGenFun hft₂

Docstring: Isomorphic finite-type weighted sets have equal weight generating functions.
(Proposition \ref{prop.gf-ws.iso}) 

## PROJECT DEPENDENCY WeightedSet (inductive)
Type u_2 → Type u_2

Body:
WeightedSet.mk : {α : Type u_2} → (α → ℕ) → WeightedSet α

Docstring: A weighted set is a type equipped with a weight function to ℕ.
(Definition \ref{def.gf-ws.weighted-sets}(a)) 

## PROJECT DEPENDENCY WeightedSet.IsFiniteType (def)
{α : Type u_2} → WeightedSet α → Prop

Body:
fun {α} W => ∀ (n : ℕ), {a | W.weight a = n}.Finite

Docstring: A weighted set is finite-type if for each n ∈ ℕ, there are only finitely many
elements of weight n. (Definition \ref{def.gf-ws.weighted-sets}(b)) 

## PROJECT DEPENDENCY WeightedSet.AreIsomorphic (def)
{α : Type u_2} → {β : Type u_3} → WeightedSet α → WeightedSet β → Prop

Body:
fun {α} {β} W₁ W₂ => Nonempty (W₁.Isomorphism W₂)

Docstring: Two weighted sets are isomorphic if there exists an isomorphism between them.
(Definition \ref{def.gf-ws.weighted-sets}(e)) 

## PROJECT DEPENDENCY WeightedSet.weightGenFun (def)
{R : Type u_1} → [CommSemiring R] → {α : Type u_2} → (W : WeightedSet α) → W.IsFiniteType → PowerSeries R

Body:
fun {R} [CommSemiring R] {α} W hft => PowerSeries.mk fun n => ↑(W.countOfWeight hft n)

Docstring: The weight generating function of a finite-type weighted set is the FPS
∑_{n ∈ ℕ} (# of elements of weight n) · x^n.
(Definition \ref{def.gf-ws.weighted-sets}(c)) 

## PROJECT DEPENDENCY WeightedSet.weight (def)
{α : Type u_2} → WeightedSet α → α → ℕ

Body:
fun α self => self.1

Docstring: The weight function assigning a natural number to each element 

## PROJECT DEPENDENCY WeightedSet.Isomorphism (inductive)
{α : Type u_2} → {β : Type u_3} → WeightedSet α → WeightedSet β → Type (max u_2 u_3)

Body:
WeightedSet.Isomorphism.mk : {α : Type u_2} →
  {β : Type u_3} →
    {W₁ : WeightedSet α} →
      {W₂ : WeightedSet β} → (toEquiv : α ≃ β) → (∀ (a : α), W₂.weight (toEquiv a) = W₁.weight a) → W₁.Isomorphism W₂

Docstring: An isomorphism between weighted sets is a weight-preserving bijection.
(Definition \ref{def.gf-ws.weighted-sets}(d)) 

## PROJECT DEPENDENCY WeightedSet.countOfWeight (def)
{α : Type u_2} → (W : WeightedSet α) → W.IsFiniteType → ℕ → ℕ

Body:
fun {α} W hft n => ⋯.toFinset.card

Docstring: For a finite-type weighted set, the count of elements of weight n 

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

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

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

## BASE-LIBRARY REF Nonempty
Sort u → Prop

Docstring: `Nonempty α` is a typeclass that says that `α` is not an empty type,
that is, there exists an element in the type. It differs from `Inhabited α`
in that `Nonempty α` is a `Prop`, which means that it does not actually carry
an element of `α`, only a proof that *there exists* such an element.
Given `Nonempty α`, you can construct an element of `α` *nonconstructively*
using `Classical.choice`.


## BASE-LIBRARY REF PowerSeries.mk
{R : Type u_2} → (ℕ → R) → PowerSeries R

Docstring: Constructor for formal power series. 

## BASE-LIBRARY REF Nat.cast
{R : Type u} → [NatCast R] → ℕ → R

Docstring: The canonical homomorphism `Nat → R`. In most use cases, the target type will have a (semi)ring
structure, and this homomorphism should be a (semi)ring homomorphism.

`NatCast` and `IntCast` exist to allow different libraries with their own types that can be notated
as natural numbers to have consistent `simp` normal forms without needing to create coercion
simplification sets that are aware of all combinations. Libraries should make it easy to work with
`NatCast` where possible. For instance, in Mathlib there will be such a homomorphism (and thus a
`NatCast R` instance) whenever `R` is an additive monoid with a `1`.

The prototypical example is `Int.ofNat`.


## BASE-LIBRARY REF AddMonoidWithOne.toNatCast
{R : Type u_2} → [self : AddMonoidWithOne R] → NatCast R

## BASE-LIBRARY REF AddCommMonoidWithOne.toAddMonoidWithOne
{R : Type u_2} → [self : AddCommMonoidWithOne R] → AddMonoidWithOne R

## BASE-LIBRARY REF NonAssocSemiring.toAddCommMonoidWithOne
{α : Type u} → [self : NonAssocSemiring α] → AddCommMonoidWithOne α

## BASE-LIBRARY REF Semiring.toNonAssocSemiring
{α : Type u} → [self : Semiring α] → NonAssocSemiring α

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Set.Finite.toFinset
{α : Type u} → {s : Set α} → s.Finite → Finset α

Docstring: Using choice, get the `Finset` that represents this `Set`. 

## INFORMAL STATEMENT
prop.gf-ws.iso

Let $A$ and $B$ be two isomorphic finite-type weighted sets. Then, $\overline{A}=\overline{B}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.coeff
def.fps.coeff

If $n\in \mathbb {N}$, and if $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right) \in K\left[\left[x\right]\right]$ is an FPS, then we define an element $\left[x^{n}\right]\mathbf{a}\in K$ by 

\[  \left[x^{n}\right]\mathbf{a}:=a_{n}.  \]

 This is called the \emph{coefficient of }$x^{n}$\emph{ in }$\mathbf{a}$, or the $n$\emph{-th coefficient} of $\mathbf{a}$, or the $x^{n}$\emph{-coefficient} of $\mathbf{a}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.fps
def.fps.fps

A \emph{formal power series} (or, short, \emph{FPS}) in $1$ indeterminate over $K$ means a sequence $\left(a_{0},a_{1},a_{2},\ldots \right) = \left(a_{n}\right)_{n\in \mathbb {N}} \in K^{\mathbb {N}}$ of elements of $K$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.ops
def.fps.ops

\textbf{(a)} The \emph{sum} of two FPSs $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right)$ and $\mathbf{b}=\left(b_{0},b_{1},b_{2},\ldots \right)$ is defined to be the FPS

\[  \left(a_{0}+b_{0},\  \  a_{1}+b_{1},\  \  a_{2}+b_{2},\  \  \ldots \right).  \]

 It is denoted by $\mathbf{a}+\mathbf{b}$. \medskip 

\textbf{(b)} The \emph{difference} of two FPSs $\mathbf{a}=\left(a_{0},a_{1},a_{2},\ldots \right)$ and $\mathbf{b}=\left(b_{0},b_{1},b_{2},\ldots \right)$ is defined to be the FPS

\[  \left(a_{0}-b_{0},\  \  a_{1}-b_{1},\  \  a_{2}-b_{2},\  \  \ldots \right).  \]

 It is denoted by $\mathbf{a}-\mathbf{b}$. \medskip 

\textbf{(c)} If $\lambda \in K$ and if $\mathbf{a}=\left(a_{0},a_{1},a_{2},\ldots \right)$ is an FPS, then we define an FPS 

\[  \lambda \mathbf{a}:=\left(\lambda a_{0},\lambda a_{1},\lambda a_{2},\ldots \right).  \]

\textbf{(d)} The \emph{product} of two FPSs $\mathbf{a}=\left(a_{0},a_{1},a_{2},\ldots \right)$ and $\mathbf{b}=\left(b_{0},b_{1},b_{2},\ldots \right)$ is defined to be the FPS $\left(c_{0},c_{1},c_{2},\ldots \right)$, where 

\begin{align*}  c_{n} &  =\sum _{i=0}^{n}a_{i}b_{n-i}=\sum _{\substack {\left(i,j\right) \in \mathbb {N}^{2};\\ \begin{bgroup} i+j=n

\end{bgroup}}}a_{i}b_{j}\\ &  =a_{0}b_{n}+a_{1}b_{n-1}+a_{2}b_{n-2}+\cdots +a_{n}b_{0}\  \  \  \  \  \  \  \  \  \  \text{for each }n\in \mathbb {N}. \end{align*}

 This product is denoted by $\mathbf{a}\cdot \mathbf{b}$ or just by $\mathbf{ab}$. \medskip 

\textbf{(e)} For each $a\in K$, we define $\underline{a}$ to be the FPS $\left(a,0,0,0,\ldots \right)$. An FPS of the form $\underline{a}$ for some $a\in K$ (that is, an FPS $\left(a_{0},a_{1},a_{2},\ldots \right)$ satisfying $a_{1}=a_{2}=a_{3}=\cdots =0$) is said to be \emph{constant}. \medskip 

\textbf{(f)} The set of all FPSs (in $1$ indeterminate over $K$) is denoted $K\left[\left[x\right]\right]$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.summable
def.fps.summable

A (possibly infinite) family $\left(\mathbf{a}_{i}\right)_{i\in I}$ of FPSs is said to be \emph{summable} (or \emph{entrywise essentially finite}) if 

\[  \text{for each }n\in \mathbb {N}\text{, all but finitely many }i\in I\text{ satisfy }\left[x^{n}\right]\mathbf{a}_{i}=0.  \]

 In this case, the sum $\sum _{i\in I}\mathbf{a}_{i}$ is defined to be the FPS with 

\[  \left[x^{n}\right]\left(\sum _{i\in I}\mathbf{a}_{i}\right) =\underbrace{\sum _{i\in I}\left[x^{n}\right]\mathbf{a}_{i}}_{\substack {\text{an essentially}\\ \text{finite sum}}} \  \  \  \  \  \  \  \  \  \  \text{for all }n\in \mathbb {N}\text{.}  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.x
def.fps.x

Let $x$ denote the FPS $\left(0,1,0,0,0,\ldots \right)$. In other words, let $x$ denote the FPS with $\left[x^{1}\right]x=1$ and $\left[x^{i}\right]x=0$ for all $i\neq 1$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.gf-ws.weighted-sets
def.gf-ws.weighted-sets

\textbf{(a)} A \emph{weighted set} is a set $A$ equipped with a function $w:A\rightarrow \mathbb {N}$, which is called the \emph{weight function} of this weighted set. For each $a\in A$, the value $w\left( a\right) $ is denoted $\left\vert a\right\vert $ and is called the \emph{weight} of $a$ (in our weighted set). \medskip 

Usually, instead of explicitly specifying the weight function $w$ as a function, we will simply specify the weight $\left\vert a\right\vert $ for each $a\in A$. The weighted set consisting of the set $A$ and the weight function $w$ will be called $\left( A,w\right) $ or simply $A$ when the weight function $w$ is clear from the context. \medskip 

\textbf{(b)} A weighted set $A$ is said to be \emph{finite-type} if for each $n\in \mathbb {N}$, there are only finitely many $a\in A$ having weight $\left\vert a\right\vert =n$. \medskip 

\textbf{(c)} If $A$ is a finite-type weighted set, then the \emph{weight generating function} of $A$ is defined to be the FPS

\[  \sum _{a\in A}x^{\left\vert a\right\vert }=\sum _{n\in \mathbb {N}}\left( \text{\#  of }a\in A\text{ having weight }n\right) \cdot x^{n}\in \mathbb {Z}\left[ \left[ x\right] \right] .  \]

 This FPS is denoted by $\overline{A}$. \medskip 

\textbf{(d)} An \emph{isomorphism} between two weighted sets $A$ and $B$ means a bijection $\rho :A\rightarrow B$ that preserves the weight (i.e., each $a\in A$ satisfies $\left\vert \rho \left( a\right) \right\vert =\left\vert a\right\vert $). \medskip 

\textbf{(e)} We say that two weighted sets $A$ and $B$ are \emph{isomorphic} (this is written $A\cong B$) if there exists an isomorphism between $A$ and $B$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.infsum.essfin
def.infsum.essfin

\textbf{(a)} A family $\left(a_{i}\right)_{i\in I}\in K^{I}$ of elements of $K$ is said to be \emph{essentially finite} if all but finitely many $i\in I$ satisfy $a_{i}=0$ (in other words, if the set $\left\{ i\in I\  \mid \  a_{i}\neq 0\right\} $ is finite). \medskip 

\textbf{(b)} Let $\left(a_{i}\right)_{i\in I}\in K^{I}$ be an essentially finite family of elements of $K$. Then, the infinite sum $\sum _{i\in I}a_{i}$ is defined to equal the finite sum $\sum _{\substack {i\in I;\\ a_{i}\neq 0}}a_{i}$. Such an infinite sum is said to be \emph{essentially finite}.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint assumes \u201ctwo isomorphic finite-type weighted sets\u201d and concludes \u201cA\u0304 = B\u0304.\u201d The Lean signature has exactly the corresponding data and hypotheses: `(W\u2081 : WeightedSet \u03b1) (W\u2082 : WeightedSet \u03b2) (hft\u2081 : W\u2081.IsFiniteType) (hft\u2082 : W\u2082.IsFiniteType), (W\u2081 \u2245\u1d65 W\u2082) \u2192 ...`. Here `IsFiniteType` means each weight fiber is finite, and `AreIsomorphic`/`\u2245\u1d65` means `Nonempty (W\u2081.Isomorphism W\u2082)`, where an isomorphism is a weight-preserving equivalence, matching the informal definitions. The conclusion `W\u2081.weightGenFun hft\u2081 = W\u2082.weightGenFun hft\u2082` is equality of the series whose nth coefficients are the cardinalities of the weight-n fibers. The additional universal choice `{R} [CommSemiring R]` makes the theorem more general than the blueprint\u2019s explicitly integer-valued generating functions: specializing to `R = \u2124` gives the stated result. Thus this is harmless strengthening, not an added restricting hypothesis."
}