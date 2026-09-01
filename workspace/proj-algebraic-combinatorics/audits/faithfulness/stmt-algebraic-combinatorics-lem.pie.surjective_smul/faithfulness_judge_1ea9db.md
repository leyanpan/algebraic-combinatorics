## TARGET AlgebraicCombinatorics.InclusionExclusion.surjective_smul (theorem) — ELABORATED SIGNATURE
∀ {m n : ℕ} (σ : Equiv.Perm (Fin n)) {f : Fin m → Fin n}, Function.Surjective f → Function.Surjective (σ • f)

Docstring: Post-composition with a permutation preserves surjectivity. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Function.Surjective
{α : Sort u_1} → {β : Sort u_2} → (α → β) → Prop

Docstring: A function `f : α → β` is called surjective if every `b : β` is equal to `f a`
for some `a : α`. 

## BASE-LIBRARY REF HSMul.hSMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSMul α β γ] → α → β → γ

Docstring: `a • b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent, but it is intended to be used for left actions. 

Conventions for notations in identifiers:

 * The recommended spelling of `•` in identifiers is `smul`.

## BASE-LIBRARY REF instHSMul
{α : Type u_1} → {β : Type u_2} → [SMul α β] → HSMul α β β

## BASE-LIBRARY REF Function.hasSMul
{ι : Type u_1} → {M : Type u_2} → {α : Type u_7} → [SMul M α] → SMul M (ι → α)

Docstring: Non-dependent version of `Pi.smul`. Lean gets confused by the dependent instance if this
is not present. 

## BASE-LIBRARY REF SemigroupAction.toSMul
{α : Type u_9} → {β : Type u_10} → {inst : Semigroup α} → [self : SemigroupAction α β] → SMul α β

## BASE-LIBRARY REF Monoid.toSemigroup
{M : Type u} → [self : Monoid M] → Semigroup M

## BASE-LIBRARY REF DivInvMonoid.toMonoid
{G : Type u} → [self : DivInvMonoid G] → Monoid G

## BASE-LIBRARY REF Group.toDivInvMonoid
{G : Type u} → [self : Group G] → DivInvMonoid G

## BASE-LIBRARY REF Equiv.Perm.permGroup
{α : Type u_4} → Group (Equiv.Perm α)

## BASE-LIBRARY REF MulAction.toSemigroupAction
{α : Type u_9} → {β : Type u_10} → {inst : Monoid α} → [self : MulAction α β] → SemigroupAction α β

## BASE-LIBRARY REF Equiv.Perm.applyMulAction
(α : Type u_6) → MulAction (Equiv.Perm α) α

Docstring: The tautological action by `Equiv.Perm α` on `α`.

This generalizes `Function.End.applyMulAction`. 

## INFORMAL STATEMENT
Post-composition preserves surjectivity

\leanhelper  If $\sigma $ is a permutation of $[n]$ and $f\colon [m] \to [n]$ is surjective, then $\sigma \circ f$ is surjective.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv-2eb59533
conv-2eb59533

In the Lean formalization, we use $\operatorname {Fin} n = \{ 0, 1, \ldots , n-1\} $ instead of the textbook’s $[n] = \{ 1, 2, \ldots , n\} $. Both are $n$-element sets, so their symmetric groups are isomorphic. Permutations are represented by the type of bijections $X \to X$ (denoted $\operatorname {Equiv.Perm}\,  X$ in Lean), which is a group under composition. Composition $\alpha \beta $ is the group multiplication $\alpha * \beta $, sending $x$ to $\alpha (\beta (x))$.

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
  "justification": "The blueprint quantifies over \u201ca permutation of [n]\u201d and a surjective map \u201cf : [m] \u2192 [n]\u201d; the elaborated binders match this as `\u03c3 : Equiv.Perm (Fin n)`, `f : Fin m \u2192 Fin n`, and `Function.Surjective f`. By `Function.hasSMul` together with `Equiv.Perm.applyMulAction`, `(\u03c3 \u2022 f)` is the pointwise action `x \u21a6 \u03c3 (f x)`, exactly the stated post-composition `\u03c3 \u2218 f`. The conclusion `Function.Surjective (\u03c3 \u2022 f)` therefore precisely says that this post-composition is surjective. The replacement of `[n]` and `[m]` by `Fin n` and `Fin m` is explicitly prescribed by the informal definition."
}