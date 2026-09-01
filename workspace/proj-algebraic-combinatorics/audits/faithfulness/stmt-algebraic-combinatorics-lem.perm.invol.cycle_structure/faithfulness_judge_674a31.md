## TARGET AlgebraicCombinatorics.involution_cycle_structure (theorem) — ELABORATED SIGNATURE
∀ {X : Type u_1} [inst : DecidableEq X] [inst_1 : Fintype X] {σ : Equiv.Perm X},
  AlgebraicCombinatorics.IsInvolution σ → ∀ c ∈ σ.cycleFactorsFinset, c.support.card ≤ 2

Docstring: The cycle digraph of an involution consists of 1-cycles and 2-cycles.
(Stated informally at the end of the source) 

## PROJECT DEPENDENCY AlgebraicCombinatorics.IsInvolution (def)
{X : Type u_1} → Equiv.Perm X → Prop

Body:
fun {X} σ => σ * σ = 1

Docstring: A permutation is an involution if `σ ∘ σ = id`. (def.perm.invol)

From the textbook:
> An *involution* of X means a map f: X → X that satisfies f ∘ f = id.
> Clearly, an involution is always a permutation, and equals its own inverse.

Equivalent characterizations:
- `IsInvolution σ ↔ σ * σ = 1` (definition)
- `IsInvolution σ ↔ σ⁻¹ = σ` (see `isInvolution_iff_eq_inv`)
- `IsInvolution σ ↔ Function.Involutive σ` (see `isInvolution_iff_involutive`)
- `IsInvolution σ ↔ ∀ x, σ (σ x) = x` (see `isInvolution_iff_forall`)


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

## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Finset.instMembership
{α : Type u_1} → Membership α (Finset α)

## BASE-LIBRARY REF Equiv.Perm.cycleFactorsFinset
{α : Type u_2} → [DecidableEq α] → [Fintype α] → Equiv.Perm α → Finset (Equiv.Perm α)

Docstring: Factors a permutation `f` into a `Finset` of disjoint cyclic permutations that multiply to `f`.


## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Equiv.Perm.support
{α : Type u_1} → [DecidableEq α] → [Fintype α] → Equiv.Perm α → Finset α

Docstring: The `Finset` of nonfixed points of a permutation. 

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

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

## BASE-LIBRARY REF Equiv.Perm.instMul
{α : Type u_4} → Mul (Equiv.Perm α)

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF Equiv.Perm.instOne
{α : Type u_4} → One (Equiv.Perm α)

## INFORMAL STATEMENT
lem.perm.invol.cycle_structure

\leanhelper  The cycle digraph of an involution of a finite set consists of $1$-cycles and $2$-cycles only. That is, every cycle factor of an involution has support of size at most~ $2$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.dcdlisttoperm
def.dcdListToPerm

\leanhelper  Given a list of lists (each representing a cycle), the corresponding permutation is obtained by composing the cycle permutations $\operatorname {cyc}_{a_1, a_2, \ldots , a_m}$ for each list $(a_1, a_2, \ldots , a_m)$ in the input.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.comps
def.fps.comps

\textbf{(a)} An \emph{(integer) composition} means a (finite) tuple of positive integers. \medskip 

\textbf{(b)} The \emph{size} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $\alpha _{1}+\alpha _{2}+\cdots +\alpha _{m}$. It is written $\left\vert \alpha \right\vert $. \medskip 

\textbf{(c)} The \emph{length} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $m$. It is written $\ell \left( \alpha \right) $. \medskip 

\textbf{(d)} Let $n\in \mathbb {N}$. A \emph{composition of }$n$ means a composition whose size is $n$. \medskip 

\textbf{(e)} Let $n\in \mathbb {N}$ and $k\in \mathbb {N}$. A \emph{composition of }$n$\emph{ into }$k$\emph{ parts} is a composition whose size is $n$ and whose length is $k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pars.parts
def.pars.parts

\textbf{(a)} An \emph{(integer) partition} means a (finite) weakly decreasing tuple of positive integers – i.e., a finite tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{m}\right) $ of positive integers such that $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{m}$. 

Thus, partitions are the same as weakly decreasing compositions. Hence, the notions of \emph{size} and \emph{length} of a partition are automatically defined, since we have defined them for compositions (in Definition \ref{def.fps.comps}). \medskip 

\textbf{(b)} The \emph{parts} of a partition $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{m}\right) $ are simply its entries $\lambda _{1},\lambda _{2},\ldots ,\lambda _{m}$. \medskip 

\textbf{(c)} Let $n\in \mathbb {Z}$. A \emph{partition of }$n$ means a partition whose size is $n$. \medskip 

\textbf{(d)} Let $n\in \mathbb {Z}$ and $k\in \mathbb {N}$. A \emph{partition of }$n$\emph{ into }$k$\emph{ parts} is a partition whose size is $n$ and whose length is $k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.cycs
def.perm.cycs

Let $X$ be a set. Let $i_1, i_2, \ldots , i_k$ be $k$ distinct elements of $X$. Then, 

\[  \operatorname {cyc}_{i_1, i_2, \ldots , i_k}  \]

 means the permutation of $X$ that sends 

\begin{align*} & i_1 \text{ to } i_2, \\ & i_2 \text{ to } i_3, \\ & \ldots , \\ & i_{k-1} \text{ to } i_k, \\ & i_k \text{ to } i_1 \end{align*}

 and leaves all other elements of $X$ unchanged. In other words, $\operatorname {cyc}_{i_1, i_2, \ldots , i_k}$ means the permutation of $X$ that satisfies 

\[  \operatorname {cyc}_{i_1, \ldots , i_k}(p) = \begin{cases}  i_{j+1}, &  \text{if } p = i_j \text{ for some } j \in \{ 1, 2, \ldots , k\} ;\\ p, &  \text{otherwise} \end{cases}  \]

 for every $p \in X$, where $i_{k+1}$ means $i_1$. 

This permutation is called a $k$\emph{-cycle}.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.cycs.cycs
def.perm.cycs.cycs

Let $X$ be a finite set. Let $\sigma $ be a permutation of $X$. \medskip 

\textbf{(a)} The \emph{cycles} of $\sigma $ are defined to be the cycles in the DCD of $\sigma $ (as defined in Theorem \ref{thm.perm.dcd.main} \textbf{(a)}). (This includes $1$-cycles, if there are any in the DCD of $\sigma $.) 

We shall equate a cycle of $\sigma $ with any of its cyclic rotations; thus, for example, $\left( 3,1,4\right) $ and $\left( 1,4,3\right) $ shall be regarded as being the same cycle (but $\left( 3,1,4\right) $ and $\left( 3,4,1\right) $ shall not). \medskip 

\textbf{(b)} The \emph{cycle lengths partition} of $\sigma $ shall denote the partition of $\left\vert X\right\vert $ obtained by writing down the lengths of the cycles of $\sigma $ in weakly decreasing order.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.invol
def.perm.invol

Let $X$ be a set. An \emph{involution} of $X$ means a map $f : X \to X$ that satisfies $f \circ f = \operatorname {id}$. Clearly, an involution is always a permutation, and equals its own inverse.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint assumes \u201can involution of a finite set\u201d and concludes that \u201cevery cycle factor of an involution has support of size at most 2.\u201d The Lean signature matches this as `\u2200 {X} [DecidableEq X] [Fintype X] {\u03c3 : Equiv.Perm X}, IsInvolution \u03c3 \u2192 \u2200 c \u2208 \u03c3.cycleFactorsFinset, c.support.card \u2264 2`. Here `[Fintype X]` encodes the stated finiteness, `Equiv.Perm X` is a permutation, and `IsInvolution \u03c3` has body `\u03c3 * \u03c3 = 1`, matching the informal condition `f \u2218 f = id`. The conclusion directly bounds every cyclic factor returned by `cycleFactorsFinset` by support cardinality at most two. The additional `[DecidableEq X]` is non-contentful finite-set infrastructure required by `cycleFactorsFinset` and `support`, rather than a mathematical restriction. Although fixed points/1-cycles may not appear as nontrivial permutation factors, their omission does not weaken the asserted upper bound: a fixed-point cycle is already a 1-cycle, while every represented nontrivial cycle factor is covered by the formal quantifier."
}