## TARGET Equiv.Perm.length_mul_swap_left (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (σ : Equiv.Perm (Fin n)) (k : Fin (n - 1)) (h : n > 1),
  (Equiv.Perm.simpleTransposition k * σ).length =
    if σ⁻¹ (Fin.castLE ⋯ k.castSucc) < σ⁻¹ (Fin.castLE ⋯ k.succ) then σ.length + 1 else σ.length - 1

Docstring: **Lemma lem.perm.len.ssl (b)**: When multiplying a permutation σ on the left by
a simple transposition s_k:
- If σ⁻¹(k) < σ⁻¹(k+1), then ℓ(s_k·σ) = ℓ(σ) + 1
- If σ⁻¹(k) > σ⁻¹(k+1), then ℓ(s_k·σ) = ℓ(σ) - 1

Note: σ⁻¹(i) is the position where i appears in the one-line notation of σ. 

## TARGET Equiv.Perm.length_mul_swap_right (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (σ : Equiv.Perm (Fin n)) (k : Fin (n - 1)) (h : n > 1),
  (σ * Equiv.Perm.simpleTransposition k).length =
    if σ (Fin.castLE ⋯ k.castSucc) < σ (Fin.castLE ⋯ k.succ) then σ.length + 1 else σ.length - 1

Docstring: **Lemma lem.perm.len.ssl (a)**: When multiplying a permutation σ on the right by
a simple transposition s_k:
- If σ(k) < σ(k+1), then ℓ(σ·s_k) = ℓ(σ) + 1
- If σ(k) > σ(k+1), then ℓ(σ·s_k) = ℓ(σ) - 1

This lemma is fundamental for understanding how length changes under composition. 

## PROJECT DEPENDENCY Equiv.Perm.length (def)
{n : ℕ} → Equiv.Perm (Fin n) → ℕ

Body:
fun {n} σ => σ.inversions.card

Docstring: The length of a permutation is the number of its inversions. 

## PROJECT DEPENDENCY Equiv.Perm.simpleTransposition (def)
{n : ℕ} → Fin (n - 1) → Equiv.Perm (Fin n)

Body:
fun {n} k => if h : n > 0 then Equiv.swap (Fin.castLE ⋯ k.castSucc) (Fin.castLE ⋯ k.succ) else 1

Docstring: The simple transposition `s_k` that swaps `k` and `k+1` in `Fin n`.
For `k : Fin (n-1)`, this swaps positions `k.castSucc` and `k.succ`.

**Note:** This is equivalent to `AlgebraicCombinatorics.simpleTransposition k` from `Basics.lean`.
See `simpleTransposition_eq_canonical` for the proof of equivalence.

**Recommended:** For new code, prefer `AlgebraicCombinatorics.simpleTransposition` (the canonical
definition). Use this definition when working with reduced words and Coxeter-style arguments
within this file. 

## PROJECT DEPENDENCY Equiv.Perm.inversions (def)
{n : ℕ} → Equiv.Perm (Fin n) → Finset (Fin n × Fin n)

Body:
fun {n} σ => {p | p.1 < p.2 ∧ σ p.2 < σ p.1}

Docstring: The set of inversions of a permutation. 

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

## BASE-LIBRARY REF GT.gt
{α : Type u} → [LT α] → α → α → Prop

Docstring: `a > b` is an abbreviation for `b < a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `>` in identifiers is `gt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

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

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTFin
{n : ℕ} → LT (Fin n)

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

## BASE-LIBRARY REF Inv.inv
{α : Type u} → [self : Inv α] → α → α

Docstring: `a⁻¹` computes the inverse of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `⁻¹` in identifiers is `inv`.

## BASE-LIBRARY REF Equiv.Perm.instInv
{α : Type u_4} → Inv (Equiv.Perm α)

## BASE-LIBRARY REF Fin.castLE
{n m : ℕ} → n ≤ m → Fin n → Fin m

Docstring: Coarsens a bound to one at least as large.

See also `Fin.castAdd` for a version that represents the larger bound with addition rather than an
explicit inequality proof.


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

## BASE-LIBRARY REF Decidable.byContradiction
∀ {p : Prop} [dec : Decidable p], (¬p → False) → p

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Nat.decLe
(n m : ℕ) → Decidable (n ≤ m)

Docstring: A decision procedure for non-strict inequality of natural numbers, usually accessed via the
`DecidableLE Nat` instance.

Examples:
 * `(if 3 ≤ 4 then "yes" else "no") = "yes"`
 * `(if 6 ≤ 4 then "yes" else "no") = "no"`
 * `show 12 ≤ 12 by decide`
 * `show 5 ≤ 12 by decide`


## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF Fin.castSucc
{n : ℕ} → Fin n → Fin (n + 1)

Docstring: Coarsens a bound by one.


## BASE-LIBRARY REF Fin.succ
{n : ℕ} → Fin n → Fin (n + 1)

Docstring: The successor, with an increased bound.

This differs from adding `1`, which instead wraps around.

Examples:
* `(2 : Fin 3).succ = (3 : Fin 4)`
* `(2 : Fin 3) + 1 = (0 : Fin 3)`


## BASE-LIBRARY REF Fin.decLt
{n : ℕ} → (a b : Fin n) → Decidable (a < b)

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF dite
{α : Sort u} → (c : Prop) → [h : Decidable c] → (c → α) → (¬c → α) → α

Docstring: "Dependent" if-then-else, normally written via the notation `if h : c then t(h) else e(h)`,
is sugar for `dite c (fun h => t(h)) (fun h => e(h))`, and it is the same as
`if c then t else e` except that `t` is allowed to depend on a proof `h : c`,
and `e` can depend on `h : ¬c`. (Both branches use the same name for the hypothesis,
even though it has different types in the two cases.)

We use this to be able to communicate the if-then-else condition to the branches.
For example, `Array.get arr i h` expects a proof `h : i < arr.size` in order to
avoid a bounds check, so you can write `if h : i < arr.size then arr.get i h else ...`
to avoid the bounds check inside the if branch. (Of course in this case we have only
lifted the check into an explicit `if`, but we could also use this proof multiple times
or derive `i < arr.size` from some other proposition that we are checking in the `if`.)


## BASE-LIBRARY REF Nat.decLt
(n m : ℕ) → Decidable (n < m)

Docstring: A decision procedure for strict inequality of natural numbers, usually accessed via the
`DecidableLT Nat` instance.

Examples:
 * `(if 3 < 4 then "yes" else "no") = "yes"`
 * `(if 4 < 4 then "yes" else "no") = "no"`
 * `(if 6 < 4 then "yes" else "no") = "no"`
 * `show 5 < 12 by decide`


## BASE-LIBRARY REF Equiv.swap
{α : Sort u_1} → [DecidableEq α] → α → α → Equiv.Perm α

Docstring: `swap a b` is the permutation that swaps `a` and `b` and
leaves other values as is. 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF Equiv.Perm.instOne
{α : Type u_4} → One (Equiv.Perm α)

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

## BASE-LIBRARY REF instDecidableAnd
{p q : Prop} → [dp : Decidable p] → [dq : Decidable q] → Decidable (p ∧ q)

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF instFintypeProd
(α : Type u_4) → (β : Type u_5) → [Fintype α] → [Fintype β] → Fintype (α × β)

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## INFORMAL STATEMENT
Single swap lemma

Let $n \in \mathbb {N}$, $\sigma \in S_n$ and $k \in [n-1]$. Then: \medskip 

\textbf{(a)} We have 

\[  \ell (\sigma s_k) = \begin{cases}  \ell (\sigma ) + 1, &  \text{if } \sigma (k) < \sigma (k+1); \\ \ell (\sigma ) - 1, &  \text{if } \sigma (k) > \sigma (k+1). \end{cases}  \]

\textbf{(b)} We have 

\[  \ell (s_k \sigma ) = \begin{cases}  \ell (\sigma ) + 1, &  \text{if } \sigma ^{-1}(k) < \sigma ^{-1}(k+1); \\ \ell (\sigma ) - 1, &  \text{if } \sigma ^{-1}(k) > \sigma ^{-1}(k+1). \end{cases}  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv-2eb59533
conv-2eb59533

In the Lean formalization, we use $\operatorname {Fin} n = \{ 0, 1, \ldots , n-1\} $ instead of the textbook’s $[n] = \{ 1, 2, \ldots , n\} $. Both are $n$-element sets, so their symmetric groups are isomorphic. Permutations are represented by the type of bijections $X \to X$ (denoted $\operatorname {Equiv.Perm}\,  X$ in Lean), which is a group under composition. Composition $\alpha \beta $ is the group multiplication $\alpha * \beta $, sending $x$ to $\alpha (\beta (x))$.

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
  "justification": "The two targets exactly match parts (a) and (b). For (a), `length_mul_swap_right` states `(\u03c3 * Equiv.Perm.simpleTransposition k).length = if \u03c3(k) < \u03c3(k+1) then \u03c3.length + 1 else \u03c3.length - 1`; for (b), `length_mul_swap_left` states `(Equiv.Perm.simpleTransposition k * \u03c3).length = if \u03c3\u207b\u00b9(k) < \u03c3\u207b\u00b9(k+1) then \u03c3.length + 1 else \u03c3.length - 1`. The embedded `Fin.castLE` terms merely place `k.castSucc` and `k.succ` in `Fin n`, implementing the zero-based counterparts of textbook indices `k` and `k+1`. The dependency bodies also agree with the blueprint: `length` is `\u03c3.inversions.card`, inversions satisfy `i < j \u2227 \u03c3 j < \u03c3 i`, and `simpleTransposition` swaps the adjacent indices. The extra binder `(h : n > 1)` is redundant rather than restrictive: the preceding binder `k : Fin (n - 1)` can exist only when `n - 1 > 0`, hence only when `n > 1`; for smaller `n` the blueprint quantification over `k \u2208 [n-1]` is vacuous. Finally, the `else` branch corresponds to the displayed `>` case because the two adjacent inputs are distinct and a permutation is injective, so their images (or inverse images) cannot be equal."
}