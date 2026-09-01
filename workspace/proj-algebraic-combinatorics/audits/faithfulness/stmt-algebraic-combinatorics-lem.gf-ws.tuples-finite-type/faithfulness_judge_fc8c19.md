## TARGET WeightedSet.tuples_isFiniteType (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_2} (W : WeightedSet α), W.IsFiniteType → W.HasPositiveWeights → W.tuples.IsFiniteType

Docstring: The tuples weighted set is finite-type if the original is finite-type and has positive weights.

Note: The hypothesis `hpos : W.HasPositiveWeights` is necessary. Without it, the theorem is false:
if W has elements of weight 0, then for any weight m, there are infinitely many tuples of weight m
(we can have arbitrarily many weight-0 elements in a tuple). For example, if W = ℕ with weight = id,
then tuples of weight 2 include ⟨1, ![2]⟩, ⟨2, ![0, 2]⟩, ⟨3, ![0, 0, 2]⟩, etc.

The key insight is that with positive weights, a tuple of length n has weight ≥ n, so for weight m,
we only need to consider tuples of length ≤ m. 

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

## PROJECT DEPENDENCY WeightedSet.HasPositiveWeights (def)
{α : Type u_2} → WeightedSet α → Prop

Body:
fun {α} W => ∀ (a : α), W.weight a ≥ 1

Docstring: A weighted set has positive weights if every element has weight ≥ 1 

## PROJECT DEPENDENCY WeightedSet.tuples (def)
{α : Type u_2} → WeightedSet α → WeightedSet ((n : ℕ) × (Fin n → α))

Body:
fun {α} W =>
  {
    weight := fun x =>
      match x with
      | ⟨n, f⟩ => ∑ i, W.weight (f i) }

Docstring: The infinite disjoint union W^0 + W^1 + W^2 + ... of all tuples of elements.
This is the "Kleene star" construction on weighted sets.
An element is a pair (k, f) where k ∈ ℕ and f : Fin k → α is a k-tuple.
The weight of (k, f) is the sum of weights of the entries: ∑ᵢ |f(i)|. 

## PROJECT DEPENDENCY WeightedSet.weight (def)
{α : Type u_2} → WeightedSet α → α → ℕ

Body:
fun α self => self.1

Docstring: The weight function assigning a natural number to each element 

## PROJECT DEPENDENCY WeightedSet.mk (constructor)
{α : Type u_2} → (α → ℕ) → WeightedSet α

## BASE-LIBRARY REF Sigma
{α : Type u} → (α → Type v) → Type (max u v)

Docstring: Dependent pairs, in which the second element's type depends on the value of the first element. The
type `Sigma β` is typically written `Σ a : α, β a` or `(a : α) × β a`.

Although its values are pairs, `Sigma` is sometimes known as the *dependent sum type*, since it is
the type level version of an indexed summation.


## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


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

## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## INFORMAL STATEMENT
lem.gf-ws.tuples-finite-type

\leanhelper  Let $A$ be a finite-type weighted set such that every element has weight $\geq 1$ (i.e., $A$ has positive weights). Then the infinite disjoint union $A^0 + A^1 + A^2 + \cdots $ (consisting of all finite tuples of elements of $A$) is also a finite-type weighted set.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-a0000000001
a0000000001

Let $A$ be a weighted set. Then, $A^{k}$ (for $k\in \mathbb {N}$) means the weighted set $\underbrace{A\times A\times \cdots \times A}_{k\text{ times}}$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.gf-ws.djun
def.gf-ws.djun

Let $A$ and $B$ be two weighted sets. Then, the weighted set $A+B$ is defined to be the disjoint union of $A$ and $B$, with the weight function inherited from $A$ and $B$ (meaning that each element of $A$ has the same weight that it had in $A$, and each element of $B$ has the same weight that it had in $B$). Formally speaking, this means that $A+B$ is the set $\left( \left\{  0\right\}  \times A\right) \cup \left( \left\{  1\right\}  \times B\right) $, with the weight function given by 

\begin{equation}  \left\vert \left( 0,a\right) \right\vert =\left\vert a\right\vert \  \  \  \  \  \  \  \  \  \  \text{for each }a\in A \end{equation}

 and

\begin{equation}  \left\vert \left( 1,b\right) \right\vert =\left\vert b\right\vert \  \  \  \  \  \  \  \  \  \  \text{for each }b\in B. \end{equation}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.gf-ws.prod
def.gf-ws.prod

Let $A$ and $B$ be two weighted sets. Then, the weighted set $A\times B$ is defined to be the Cartesian product of the sets $A$ and $B$ (that is, the set $\left\{  \left( a,b\right) \  \mid \  a\in A\text{ and }b\in B\right\}  $), with the weight function defined as follows: For any $\left( a,b\right) \in A\times B$, we set

\begin{equation}  \left\vert \left( a,b\right) \right\vert =\left\vert a\right\vert +\left\vert b\right\vert . \end{equation}

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
  "justification": "The elaborated signature, `\u2200 {\u03b1 : Type u_2} (W : WeightedSet \u03b1), W.IsFiniteType \u2192 W.HasPositiveWeights \u2192 W.tuples.IsFiniteType`, exactly matches: \u201cLet A be a finite-type weighted set such that every element has weight \u2265 1 ... Then ... all finite tuples ... is also a finite-type weighted set.\u201d The dependency bodies preserve each meaning: `IsFiniteType` is `\u2200 n, {a | W.weight a = n}.Finite`; `HasPositiveWeights` is `\u2200 a, W.weight a \u2265 1`; and `tuples` has carrier `(n : \u2115) \u00d7 (Fin n \u2192 \u03b1)` with weight `\u2211 i, W.weight (f i)`, which represents the disjoint union of all finite powers, including the unique empty tuple at `n = 0`. There are no additional mathematically contentful hypotheses or narrowed quantifiers."
}