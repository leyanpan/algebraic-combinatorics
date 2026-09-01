## TARGET WeightedSet.disjointUnion (def) — ELABORATED SIGNATURE
{α : Type u_2} → {β : Type u_3} → WeightedSet α → WeightedSet β → WeightedSet (α ⊕ β)

Body:
fun {α} {β} W₁ W₂ => { weight := Sum.elim W₁.weight W₂.weight }

Docstring: The disjoint union of two weighted sets, with weights inherited from each component.
(Definition \ref{def.gf-ws.djun}) 

## PROJECT DEPENDENCY WeightedSet (inductive)
Type u_2 → Type u_2

Body:
WeightedSet.mk : {α : Type u_2} → (α → ℕ) → WeightedSet α

Docstring: A weighted set is a type equipped with a weight function to ℕ.
(Definition \ref{def.gf-ws.weighted-sets}(a)) 

## PROJECT DEPENDENCY WeightedSet.mk (constructor)
{α : Type u_2} → (α → ℕ) → WeightedSet α

## PROJECT DEPENDENCY WeightedSet.weight (def)
{α : Type u_2} → WeightedSet α → α → ℕ

Body:
fun α self => self.1

Docstring: The weight function assigning a natural number to each element 

## BASE-LIBRARY REF Sum
Type u → Type v → Type (max u v)

Docstring: The disjoint union of types `α` and `β`, ordinarily written `α ⊕ β`.

An element of `α ⊕ β` is either an `a : α` wrapped in `Sum.inl` or a `b : β` wrapped in `Sum.inr`.
`α ⊕ β` is not equivalent to the set-theoretic union of `α` and `β` because its values include an
indication of which of the two types was chosen. The union of a singleton set with itself contains
one element, while `Unit ⊕ Unit` contains distinct values `inl ()` and `inr ()`.


## BASE-LIBRARY REF Sum.elim
{α : Type u_1} → {β : Type u_2} → {γ : Sort u_3} → (α → γ) → (β → γ) → α ⊕ β → γ

Docstring: Case analysis for sums that applies the appropriate function `f` or `g` after checking which
constructor is present.


## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## INFORMAL STATEMENT
def.gf-ws.djun

Let $A$ and $B$ be two weighted sets. Then, the weighted set $A+B$ is defined to be the disjoint union of $A$ and $B$, with the weight function inherited from $A$ and $B$ (meaning that each element of $A$ has the same weight that it had in $A$, and each element of $B$ has the same weight that it had in $B$). Formally speaking, this means that $A+B$ is the set $\left( \left\{  0\right\}  \times A\right) \cup \left( \left\{  1\right\}  \times B\right) $, with the weight function given by 

\begin{equation}  \left\vert \left( 0,a\right) \right\vert =\left\vert a\right\vert \  \  \  \  \  \  \  \  \  \  \text{for each }a\in A \end{equation}

 and

\begin{equation}  \left\vert \left( 1,b\right) \right\vert =\left\vert b\right\vert \  \  \  \  \  \  \  \  \  \  \text{for each }b\in B. \end{equation}

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
  "justification": "The blueprint defines the carrier as the tagged disjoint union \u201c({0} \u00d7 A) \u222a ({1} \u00d7 B)\u201d and requires each component\u2019s weights to be inherited. The formal declaration takes arbitrary weighted sets, `{\u03b1 : Type u_2} \u2192 {\u03b2 : Type u_3} \u2192 WeightedSet \u03b1 \u2192 WeightedSet \u03b2`, and returns `WeightedSet (\u03b1 \u2295 \u03b2)`. By the documented meaning of `Sum`, `\u03b1 \u2295 \u03b2` is exactly a tagged disjoint union. Its body sets `weight := Sum.elim W\u2081.weight W\u2082.weight`, so an `inl a` receives `W\u2081.weight a` and an `inr b` receives `W\u2082.weight b`, exactly matching the two displayed weight equations. There are no added hypotheses or restricted quantifiers."
}