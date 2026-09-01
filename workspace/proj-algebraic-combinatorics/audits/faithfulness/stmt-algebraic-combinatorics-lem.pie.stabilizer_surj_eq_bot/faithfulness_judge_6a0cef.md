## TARGET AlgebraicCombinatorics.InclusionExclusion.stabilizer_surj_eq_bot (theorem) — ELABORATED SIGNATURE
∀ {m n : ℕ} (f : { f // Function.Surjective f }), MulAction.stabilizer (Equiv.Perm (Fin n)) f = ⊥

Docstring: The action of `Perm (Fin n)` on surjective maps is free: the stabilizer of any
surjective map is trivial. This is because if `σ ∘ f = f` and `f` is surjective, then `σ = id`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.InclusionExclusion.permActionOnSurj (def)
(m n : ℕ) → MulAction (Equiv.Perm (Fin n)) { f // Function.Surjective f }

Body:
fun m n => { smul := fun σ f => ⟨σ • ↑f, ⋯⟩, mul_smul := ⋯, one_smul := ⋯ }

Docstring: Action of `Perm (Fin n)` on surjective functions `Fin m → Fin n` by post-composition. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Subtype
{α : Sort u} → (α → Prop) → Sort (max 1 u)

Docstring: All the elements of a type that satisfy a predicate.

`Subtype p`, usually written `{ x : α // p x }` or `{ x // p x }`, contains all elements `x : α` for
which `p x` is true. Its constructor is a pair of the value and the proof that it satisfies the
predicate. In run-time code, `{ x : α // p x }` is represented identically to `α`.

There is a coercion from `{ x : α // p x }` to `α`, so elements of a subtype may be used where the
underlying type is expected.

Examples:
 * `{ n : Nat // n % 2 = 0 }` is the type of even numbers.
 * `{ xs : Array String // xs.size = 5 }` is the type of arrays with five `String`s.
 * Given `xs : List α`, `List { x : α // x ∈ xs }` is the type of lists in which all elements are
   contained in `xs`.


Conventions for notations in identifiers:

 * The recommended spelling of `{ x // p x }` in identifiers is `subtype`.

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Function.Surjective
{α : Sort u_1} → {β : Sort u_2} → (α → β) → Prop

Docstring: A function `f : α → β` is called surjective if every `b : β` is equal to `f a`
for some `a : α`. 

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

## BASE-LIBRARY REF Subgroup
(G : Type u_3) → [Group G] → Type u_3

Docstring: A subgroup of a group `G` is a subset containing 1, closed under multiplication
and closed under multiplicative inverse. 

## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF Equiv.Perm.permGroup
{α : Type u_4} → Group (Equiv.Perm α)

## BASE-LIBRARY REF MulAction.stabilizer
(G : Type u_1) → {α : Type u_2} → [inst : Group G] → [MulAction G α] → α → Subgroup G

Docstring: The stabilizer of an element under an action, i.e. what sends the element to itself.
A subgroup. 

## BASE-LIBRARY REF Bot.bot
{α : Type u_1} → [self : Bot α] → α

Docstring: The bot (`⊥`, `\bot`) element 

Conventions for notations in identifiers:

 * The recommended spelling of `⊥` in identifiers is `bot`.

## BASE-LIBRARY REF Subgroup.instBot
{G : Type u_1} → [inst : Group G] → Bot (Subgroup G)

Docstring: The trivial subgroup `{1}` of a group `G`. 

## BASE-LIBRARY REF MulAction
(α : Type u_9) → Type u_10 → [Monoid α] → Type (max u_10 u_9)

Docstring: Type class for monoid actions on types, with notation `g • p`.

The `MulAction G P` typeclass says that the monoid `G` acts multiplicatively on a type `P`.
More precisely this means that the action satisfies the two axioms `1 • p = p` and
`(g₁ * g₂) • p = g₁ • (g₂ • p)`. A mathematician might simply say that the monoid `G`
acts on `P`.

For example, if `G` is a group and `X` is a type, if a mathematician says
say "let `G` act on the set `X`" they will probably mean  `[AddAction G X]`.


## BASE-LIBRARY REF DivInvMonoid.toMonoid
{G : Type u} → [self : DivInvMonoid G] → Monoid G

## BASE-LIBRARY REF Group.toDivInvMonoid
{G : Type u} → [self : Group G] → DivInvMonoid G

## BASE-LIBRARY REF MulAction.mk
{α : Type u_9} →
  {β : Type u_10} →
    [inst : Monoid α] → [toSemigroupAction : SemigroupAction α β] → (∀ (b : β), 1 • b = b) → MulAction α β

## BASE-LIBRARY REF SemigroupAction.mk
{α : Type u_9} →
  {β : Type u_10} →
    [inst : Semigroup α] → [toSMul : SMul α β] → (∀ (x y : α) (b : β), (x * y) • b = x • y • b) → SemigroupAction α β

## BASE-LIBRARY REF Monoid.toSemigroup
{M : Type u} → [self : Monoid M] → Semigroup M

## BASE-LIBRARY REF SMul.mk
{M : Type u} → {α : Type v} → (M → α → α) → SMul M α

## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

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

## BASE-LIBRARY REF MulAction.toSemigroupAction
{α : Type u_9} → {β : Type u_10} → {inst : Monoid α} → [self : MulAction α β] → SemigroupAction α β

## BASE-LIBRARY REF Equiv.Perm.applyMulAction
(α : Type u_6) → MulAction (Equiv.Perm α) α

Docstring: The tautological action by `Equiv.Perm α` on `α`.

This generalizes `Function.End.applyMulAction`. 

## BASE-LIBRARY REF Subtype.val
{α : Sort u} → {p : α → Prop} → Subtype p → α

Docstring: The value in the underlying type that satisfies the predicate.


## INFORMAL STATEMENT
Free action on surjections

\leanhelper  Let $f\colon [m] \to [n]$ be surjective. Then the stabilizer of $f$ under the action of $S_n$ by post-composition is trivial.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv-2eb59533
conv-2eb59533

In the Lean formalization, we use $\operatorname {Fin} n = \{ 0, 1, \ldots , n-1\} $ instead of the textbook’s $[n] = \{ 1, 2, \ldots , n\} $. Both are $n$-element sets, so their symmetric groups are isomorphic. Permutations are represented by the type of bijections $X \to X$ (denoted $\operatorname {Equiv.Perm}\,  X$ in Lean), which is a group under composition. Composition $\alpha \beta $ is the group multiplication $\alpha * \beta $, sending $x$ to $\alpha (\beta (x))$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.sf.kn
conv.sf.KN

Fix a commutative ring $K$. Fix an $N\in \mathbb {N}$. Throughout this chapter, we will keep $K$ and $N$ fixed. Let $S_N$ denote the symmetric group, i.e., the group of all permutations of $[N] := \{ 1,2,\ldots ,N\} $.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.sn-iven
def.perm.Sn-iven

Let $n \in \mathbb {Z}$. Then, $[n]$ shall mean the set $\{ 1, 2, \ldots , n\} $. This is an $n$-element set if $n \ge 0$, and is an empty set if $n \le 0$. 

The symmetric group $S_{[n]}$ (consisting of all permutations of $[n]$) will be denoted $S_n$ and called the $n$\emph{-th symmetric group}. Its size is $n!$ (when $n \ge 0$).

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target quantifies over arbitrary naturals and a surjective function via `\u2200 {m n : \u2115} (f : { f // Function.Surjective f })`, matching \u201cLet `f : [m] \u2192 [n]` be surjective,\u201d with `Fin m` and `Fin n` supplied by the stated Lean convention. The conclusion `MulAction.stabilizer (Equiv.Perm (Fin n)) f = \u22a5` says exactly that its stabilizer in the symmetric group is the trivial subgroup, since `Equiv.Perm (Fin n)` represents `S_n` and `Subgroup.instBot` defines `\u22a5` as `{1}`. Finally, `permActionOnSurj` defines the action by `smul := fun \u03c3 f => \u27e8\u03c3 \u2022 \u2191f, \u2026\u27e9`; together with the pointwise function action and the tautological permutation action, this is post-composition by `\u03c3`, as required. The fixed commutative ring context is irrelevant to this statement, so its absence does not narrow or alter the claim."
}