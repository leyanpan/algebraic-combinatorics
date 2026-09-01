## TARGET Equiv.Perm.alternatingGroup_isNormal (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_1} [inst : DecidableEq α] [inst_1 : Fintype α], (alternatingGroup α).Normal

Docstring: **Corollary (cor.perm.altgp)**
The set of all even permutations in Sₙ is a normal subgroup.
This is the alternating group Aₙ. 

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

## BASE-LIBRARY REF Subgroup.Normal
{G : Type u_1} → [inst : Group G] → Subgroup G → Prop

Docstring: A subgroup `H` is normal if whenever `n ∈ H`, then `g * n * g⁻¹ ∈ H` for every `g : G` 

## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF Equiv.Perm.permGroup
{α : Type u_4} → Group (Equiv.Perm α)

## BASE-LIBRARY REF alternatingGroup
(α : Type u_1) → [Fintype α] → [DecidableEq α] → Subgroup (Equiv.Perm α)

Docstring: The alternating group on a finite type, realized as a subgroup of `Equiv.Perm`.
For $A_n$, use `alternatingGroup (Fin n)`. 

## INFORMAL STATEMENT
cor.perm.altgp

Let $n \in \mathbb {N}$. The set of all even permutations in $S_n$ is a normal subgroup of $S_n$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.even-odd
def.perm.even-odd

Let $n \in \mathbb {N}$. A permutation $\sigma \in S_n$ is said to be 

\begin{itemize} \item \emph{even} if $(-1)^{\sigma } = 1$ (that is, if $\ell (\sigma )$ is even); 

\item \emph{odd} if $(-1)^{\sigma } = -1$ (that is, if $\ell (\sigma )$ is odd). 

\end{itemize}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.invs
def.perm.invs

Let $n\in \mathbb {N}$ and $\sigma \in S_{n}$. \medskip 

\textbf{(a)} An \emph{inversion} of $\sigma $ means a pair $\left(i,j\right)$ of elements of $\left[n\right]$ such that $i<j$ and $\sigma \left(i\right) >\sigma \left(j\right)$. \medskip 

\textbf{(b)} The \emph{length} (also known as the \emph{Coxeter length}) of $\sigma $ is the \#  of inversions of $\sigma $. It is called $\ell \left( \sigma \right)$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.sign
def.perm.sign

Let $n \in \mathbb {N}$. The \emph{sign} of a permutation $\sigma \in S_n$ is defined to be the integer $(-1)^{\ell (\sigma )}$. 

It is denoted by $(-1)^{\sigma }$ or $\operatorname {sgn}(\sigma )$ or $\operatorname {sign}(\sigma )$ or $\varepsilon (\sigma )$. It is also known as the \emph{signature} of $\sigma $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.sn-iven
def.perm.Sn-iven

Let $n \in \mathbb {Z}$. Then, $[n]$ shall mean the set $\{ 1, 2, \ldots , n\} $. This is an $n$-element set if $n \ge 0$, and is an empty set if $n \le 0$. 

The symmetric group $S_{[n]}$ (consisting of all permutations of $[n]$) will be denoted $S_n$ and called the $n$\emph{-th symmetric group}. Its size is $n!$ (when $n \ge 0$).

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target states `\u2200 {\u03b1 : Type u_1} [DecidableEq \u03b1] [Fintype \u03b1], (alternatingGroup \u03b1).Normal`. By the supplied docstrings, `alternatingGroup \u03b1` is the alternating group on the finite type `\u03b1`, and `Subgroup.Normal` means closure under conjugation, exactly the assertion that it is a normal subgroup. Taking `\u03b1 = Fin n` gives the blueprint\u2019s `S_n`/`A_n` case for every `n \u2208 \u2115`. Quantifying over every finite type is strictly more general than quantifying over the standard `n`-element sets, so this strengthening is faithful. The `[Fintype \u03b1]` and `[DecidableEq \u03b1]` binders provide the finite, computable setting required by `alternatingGroup`; they do not exclude any `Fin n` case."
}