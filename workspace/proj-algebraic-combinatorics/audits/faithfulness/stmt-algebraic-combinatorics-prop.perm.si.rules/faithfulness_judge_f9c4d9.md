## TARGET AlgebraicCombinatorics.simpleTransposition_braid (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (i : Fin (n - 2)),
  have i' := ⟨↑i, ⋯⟩;
  have i1 := ⟨↑i + 1, ⋯⟩;
  AlgebraicCombinatorics.simpleTransposition i' * AlgebraicCombinatorics.simpleTransposition i1 *
      AlgebraicCombinatorics.simpleTransposition i' =
    AlgebraicCombinatorics.simpleTransposition i1 * AlgebraicCombinatorics.simpleTransposition i' *
      AlgebraicCombinatorics.simpleTransposition i1

Docstring: The braid relation: `s_i s_{i+1} s_i = s_{i+1} s_i s_{i+1}`. (prop.perm.si.rules (c)) 

## TARGET AlgebraicCombinatorics.simpleTransposition_comm (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (i j : Fin (n - 1)),
  ↑i + 1 < ↑j ∨ ↑j + 1 < ↑i →
    AlgebraicCombinatorics.simpleTransposition i * AlgebraicCombinatorics.simpleTransposition j =
      AlgebraicCombinatorics.simpleTransposition j * AlgebraicCombinatorics.simpleTransposition i

Docstring: Simple transpositions commute when `|i - j| > 1`. (prop.perm.si.rules (b)) 

## TARGET AlgebraicCombinatorics.simpleTransposition_sq_eq_one (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (i : Fin (n - 1)),
  AlgebraicCombinatorics.simpleTransposition i * AlgebraicCombinatorics.simpleTransposition i = 1

Docstring: Simple transpositions are involutions: `s_i² = id`. (prop.perm.si.rules (a)) 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Sn (def)
ℕ → Type

Body:
fun n => Equiv.Perm (Fin n)

Docstring: The n-th symmetric group `S_n` is the group of permutations of `[n]`.
    (def.perm.Sn-iven)

In the textbook, `S_n` is defined as `S_[n]`, the symmetric group of `[n] = {1, 2, ..., n}`.
In Lean, we represent this as `Equiv.Perm (Fin n)`, the group of permutations of
`Fin n = {0, 1, ..., n-1}`.

The size of `S_n` is `n!` (see `sn_card`). 

## PROJECT DEPENDENCY AlgebraicCombinatorics.simpleTransposition (def)
{n : ℕ} → Fin (n - 1) → AlgebraicCombinatorics.Sn n

Body:
fun {n} i => Equiv.swap ⟨↑i, ⋯⟩ ⟨↑i + 1, ⋯⟩

Docstring: The simple transposition `s_i` swaps `i` and `i+1` in `Fin n`.
Here `i : Fin (n - 1)` ensures `i+1 < n`.
(def.perm.si)

**This is the canonical definition** for simple transpositions in the codebase.

**Equivalent definition in Inversions2.lean:**
`Equiv.Perm.simpleTransposition` in `Inversions2.lean` defines the same permutation
using a slightly different construction (with `castSucc`/`succ`). The equivalence is
proven by `Equiv.Perm.simpleTransposition_eq_canonical`.

See the equivalence lemmas `simpleTransposition_eq_swap_*` below for other formulations. 

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


## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF instSubNat
Sub ℕ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Fin.mk
{n : ℕ} → (val : ℕ) → val < n → Fin n

Docstring: Creates a `Fin n` from `i : Nat` and a proof that `i < n`. 

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## BASE-LIBRARY REF Decidable.byContradiction
∀ {p : Prop} [dec : Decidable p], (¬p → False) → p

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF Nat.decLt
(n m : ℕ) → Decidable (n < m)

Docstring: A decision procedure for strict inequality of natural numbers, usually accessed via the
`DecidableLT Nat` instance.

Examples:
 * `(if 3 < 4 then "yes" else "no") = "yes"`
 * `(if 4 < 4 then "yes" else "no") = "no"`
 * `(if 6 < 4 then "yes" else "no") = "no"`
 * `show 5 < 12 by decide`


## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF instAddNat
Add ℕ

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

## BASE-LIBRARY REF Or
Prop → Prop → Prop

Docstring: `Or a b`, or `a ∨ b`, is the disjunction of propositions. There are two
constructors for `Or`, called `Or.inl : a → a ∨ b` and `Or.inr : b → a ∨ b`,
and you can use `match` or `cases` to destruct an `Or` assumption into the
two cases.


Conventions for notations in identifiers:

 * The recommended spelling of `∨` in identifiers is `or`.

 * The recommended spelling of `\/` in identifiers is `or` (prefer `∨` over `\/`).

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF Equiv.Perm.instOne
{α : Type u_4} → One (Equiv.Perm α)

## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF Equiv.swap
{α : Sort u_1} → [DecidableEq α] → α → α → Equiv.Perm α

Docstring: `swap a b` is the permutation that swaps `a` and `b` and
leaves other values as is. 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## INFORMAL STATEMENT
prop.perm.si.rules

Let $n \in \mathbb {N}$. 

\textbf{(a)} We have $s_i^2 = \operatorname {id}$ for all $i \in [n-1]$. In other words, we have $s_i = s_i^{-1}$ for all $i \in [n-1]$. 

\textbf{(b)} We have $s_i s_j = s_j s_i$ for any $i, j \in [n-1]$ with $|i - j| > 1$. 

\textbf{(c)} We have $s_i s_{i+1} s_i = s_{i+1} s_i s_{i+1}$ for any $i \in [n-2]$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.perm.simple
conv.perm.simple

A \emph{simple transposition} in $S_n$ means one of the $n-1$ transpositions $s_0, s_1, \ldots , s_{n-2}$. We shall occasionally abbreviate “simple transposition” as “simple”.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.si
def.perm.si

Let $n \in \mathbb {N}$ and $i \in [n-1]$. Then, the \emph{simple transposition} $s_i$ is defined by 

\[  s_i := t_{i, i+1} \in S_n.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.sn-iven
def.perm.Sn-iven

Let $n \in \mathbb {Z}$. Then, $[n]$ shall mean the set $\{ 1, 2, \ldots , n\} $. This is an $n$-element set if $n \ge 0$, and is an empty set if $n \le 0$. 

The symmetric group $S_{[n]}$ (consisting of all permutations of $[n]$) will be denoted $S_n$ and called the $n$\emph{-th symmetric group}. Its size is $n!$ (when $n \ge 0$).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.tij
def.perm.tij

Let $i$ and $j$ be two distinct elements of a set $X$. 

Then, the \emph{transposition} $t_{i,j}$ is the permutation of $X$ that sends $i$ to $j$, sends $j$ to $i$, and leaves all other elements of $X$ unchanged.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The three declarations exactly encode the three relations, up to the documented zero-based representation of the textbook sets. For (a), `\u2200 {n : \u2115} (i : Fin (n - 1)), simpleTransposition i * simpleTransposition i = 1` matches \u201c`s_i^2 = id` for all `i \u2208 [n-1]`\u201d; in the permutation group, `1` is the identity. For (b), the binders `i j : Fin (n - 1)` give the required index range, and `\u2191i + 1 < \u2191j \u2228 \u2191j + 1 < \u2191i` is equivalent over naturals to `|i-j| > 1`, yielding exactly the stated commutation equality. For (c), `i : Fin (n - 2)` and the locally constructed indices with values `\u2191i` and `\u2191i + 1` give precisely `s_i s_{i+1} s_i = s_{i+1} s_i s_{i+1}`. The project definitions `Sn n := Equiv.Perm (Fin n)` and `simpleTransposition i := Equiv.swap \u27e8\u2191i,\u2026\u27e9 \u27e8\u2191i+1,\u2026\u27e9` implement the textbook objects after shifting `[n]={1,\u2026,n}` to `Fin n={0,\u2026,n-1}`. Saturating natural subtraction only makes the relevant `Fin` index types empty in the same small-`n` cases where the textbook index sets are empty."
}