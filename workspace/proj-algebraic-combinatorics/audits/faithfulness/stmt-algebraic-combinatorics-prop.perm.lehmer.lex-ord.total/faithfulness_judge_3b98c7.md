## TARGET AlgebraicCombinatorics.lexLt_trichotomous (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (a b : Fin n → ℤ), a ≠ b → AlgebraicCombinatorics.lexLt a b ∨ AlgebraicCombinatorics.lexLt b a

Docstring: If a and b are two distinct n-tuples of integers, then either a <_lex b or b <_lex a.

See Proposition 1.3.9 (prop.perm.lehmer.lex-ord.total) in the source.


## PROJECT DEPENDENCY AlgebraicCombinatorics.lexLt (def)
{n : ℕ} → (Fin n → ℤ) → (Fin n → ℤ) → Prop

Body:
fun {n} a b => ∃ k, (∀ i < k, a i = b i) ∧ a k < b k

Docstring: Lexicographic order on n-tuples of integers.
We say (a_1, ..., a_n) <_lex (b_1, ..., b_n) if there exists k ∈ [n]
such that a_k ≠ b_k and the smallest such k satisfies a_k < b_k.

Note: This is essentially `Pi.Lex (· < ·) (· < ·)` from Mathlib, specialized to `Fin n → ℤ`.
We define it directly here to match the source presentation.

See Definition 1.3.8 (def.perm.lehmer.lex-ord) in the source.


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


## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

## BASE-LIBRARY REF Or
Prop → Prop → Prop

Docstring: `Or a b`, or `a ∨ b`, is the disjunction of propositions. There are two
constructors for `Or`, called `Or.inl : a → a ∨ b` and `Or.inr : b → a ∨ b`,
and you can use `match` or `cases` to destruct an `Or` assumption into the
two cases.


Conventions for notations in identifiers:

 * The recommended spelling of `∨` in identifiers is `or`.

 * The recommended spelling of `\/` in identifiers is `or` (prefer `∨` over `\/`).

## BASE-LIBRARY REF Exists
{α : Sort u} → (α → Prop) → Prop

Docstring: Existential quantification. If `p : α → Prop` is a predicate, then `∃ x : α, p x`
asserts that there is some `x` of type `α` such that `p x` holds.
To create an existential proof, use the `exists` tactic,
or the anonymous constructor notation `⟨x, h⟩`.
To unpack an existential, use `cases h` where `h` is a proof of `∃ x : α, p x`,
or `let ⟨x, hx⟩ := h` where `.

Because Lean has proof irrelevance, any two proofs of an existential are
definitionally equal. One consequence of this is that it is impossible to recover the
witness of an existential from the mere fact of its existence.
For example, the following does not compile:
```
example (h : ∃ x : Nat, x = x) : Nat :=
  let ⟨x, _⟩ := h  -- fail, because the goal is `Nat : Type`
  x
```
The error message `recursor 'Exists.casesOn' can only eliminate into Prop` means
that this only works when the current goal is another proposition:
```
example (h : ∃ x : Nat, x = x) : True :=
  let ⟨x, _⟩ := h  -- ok, because the goal is `True : Prop`
  trivial
```


## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTFin
{n : ℕ} → LT (Fin n)

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

## BASE-LIBRARY REF Int.instLTInt
LT ℤ

## INFORMAL STATEMENT
prop.perm.lehmer.lex-ord.total

If $\mathbf{a}$ and $\mathbf{b}$ are two distinct $n$-tuples of integers, then we have either $\mathbf{a} <_{\operatorname {lex}}\mathbf{b}$ or $\mathbf{b}<_{\operatorname {lex}} \mathbf{a}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.lehmer.lex-ord
def.perm.lehmer.lex-ord

Let $\left(a_{1},a_{2},\ldots ,a_{n}\right)$ and $\left(b_{1},b_{2},\ldots ,b_{n}\right)$ be two $n$-tuples of integers. We say that 

\[  \left(a_{1},a_{2},\ldots ,a_{n}\right) <_{\operatorname {lex}}\left( b_{1},b_{2},\ldots ,b_{n}\right)  \]

 if and only if 

\begin{itemize} \item there exists some $k\in \left[n\right]$ such that $a_{k}\neq b_{k}$, and 

\item the \textbf{smallest} such $k$ satisfies $a_{k}<b_{k}$. 

\end{itemize}

 The relation $<_{\operatorname {lex}}$ is a strict total order on $\mathbb {Z}^n$ (the lexicographic order).

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
  "justification": "The target quantifies over two integer n-tuples as functions, `\u2200 {n : \u2115} (a b : Fin n \u2192 \u2124)`, assumes exactly that they are distinct, `a \u2260 b`, and concludes the required disjunction, `lexLt a b \u2228 lexLt b a`. The dependency defines `lexLt a b` as `\u2203 k, (\u2200 i < k, a i = b i) \u2227 a k < b k`: all earlier coordinates agree, while the first differing coordinate satisfies `a k < b k`. This is equivalent to the informal definition using the smallest `k \u2208 [n]` with `a_k \u2260 b_k`. Representing the coordinates `1,\u2026,n` by the zero-based type `Fin n` is an indexing encoding and does not change the mathematical claim."
}