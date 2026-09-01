## TARGET AlgebraicCombinatorics.Perm.card_invCount_symm (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (k : ℤ),
  {σ | ↑(AlgebraicCombinatorics.Perm.invCount σ) = k}.card =
    {σ | ↑(AlgebraicCombinatorics.Perm.invCount σ) = ↑(n.choose 2) - k}.card

Docstring: The number of σ ∈ S_n with ℓ(σ) = k equals the number with ℓ(σ) = (n choose 2) - k.
This is the symmetry of the length distribution.

See Proposition 1.3.3 (prop.perm.lengths-k-small-k) part (f) in the source.


## PROJECT DEPENDENCY AlgebraicCombinatorics.Perm.invCount (def)
{n : ℕ} → Equiv.Perm (Fin n) → ℕ

Body:
fun {n} σ => (AlgebraicCombinatorics.Perm.inv σ).card

Docstring: The length (or Coxeter length) of a permutation σ is the number of inversions of σ.
This is denoted ℓ(σ) in the source.

See Definition 1.3.1 (def.perm.invs) part (b) in the source.


## PROJECT DEPENDENCY AlgebraicCombinatorics.Perm.inv (def)
{n : ℕ} → Equiv.Perm (Fin n) → Finset (Fin n × Fin n)

Body:
fun {n} σ => {p | p.1 < p.2 ∧ σ p.1 > σ p.2}

Docstring: An inversion of a permutation σ ∈ S_n is a pair (i, j) of elements of [n]
such that i < j and σ(i) > σ(j).

See Definition 1.3.1 (def.perm.invs) in the source.


## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


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

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

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


## BASE-LIBRARY REF instNatCastInt
NatCast ℤ

## BASE-LIBRARY REF Int.instDecidableEq
DecidableEq ℤ

Docstring: Decides whether two integers are equal. Usually accessed via the `DecidableEq Int` instance.

This function is overridden by the compiler with an efficient implementation. This definition is the
logical model.

Examples:
* `show (7 : Int) = (3 : Int) + (4 : Int) by decide`
* `if (6 : Int) = (3 : Int) * (2 : Int) then "yes" else "no" = "yes"`
* `(¬ (6 : Int) = (3 : Int)) = true`


## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Equiv.instFintype
{α : Type u_1} → {β : Type u_2} → [DecidableEq α] → [DecidableEq β] → [Fintype α] → [Fintype β] → Fintype (α ≃ β)

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF Int.instSub
Sub ℤ

## BASE-LIBRARY REF Nat.choose
ℕ → ℕ → ℕ

Docstring: `choose n k` is the number of `k`-element subsets in an `n`-element set. Also known as binomial
coefficients. For the fact that this is the number of `k`-element-subsets of an `n`-element
set, see `Finset.card_powersetCard`. 

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

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

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

## BASE-LIBRARY REF GT.gt
{α : Type u} → [LT α] → α → α → Prop

Docstring: `a > b` is an abbreviation for `b < a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `>` in identifiers is `gt`.

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

## BASE-LIBRARY REF instDecidableAnd
{p q : Prop} → [dp : Decidable p] → [dq : Decidable q] → Decidable (p ∧ q)

## BASE-LIBRARY REF Fin.decLt
{n : ℕ} → (a b : Fin n) → Decidable (a < b)

## BASE-LIBRARY REF instFintypeProd
(α : Type u_4) → (β : Type u_5) → [Fintype α] → [Fintype β] → Fintype (α × β)

## INFORMAL STATEMENT
prop.perm.lengths-k-small-k

Let $n\in \mathbb {N}$. \medskip 

\textbf{(a)} For any $\sigma \in S_{n}$, we have $\ell \left(\sigma \right) \in \left\{ 0,1,\ldots ,\binom {n}{2}\right\} $.   \medskip 

\textbf{(b)} We have 

\[  \left(\text{\#  of }\sigma \in S_{n}\text{ with }\ell \left(\sigma \right) =0\right) = 1.  \]

 Indeed, the only permutation $\sigma \in S_{n}$ with $\ell \left( \sigma \right)=0$ is the identity map $\operatorname {id}$.   \medskip 

\textbf{(c)} We have 

\[  \left(\text{\#  of }\sigma \in S_{n}\text{ with }\ell \left(\sigma \right) =\binom {n}{2}\right) = 1.  \]

 Indeed, the only permutation $\sigma \in S_{n}$ with $\ell \left( \sigma \right)=\binom {n}{2}$ is the permutation with OLN $n\left( n-1\right)\left(n-2\right)\cdots 21$, often called~ $w_{0}$.   \medskip 

\textbf{(d)} If $n\geq 1$, then 

\[  \left(\text{\#  of }\sigma \in S_{n}\text{ with }\ell \left(\sigma \right) =1\right) = n-1.  \]

 Indeed, the only permutations $\sigma \in S_{n}$ with $\ell \left( \sigma \right)=1$ are the simple transpositions $s_{i}$ with $i\in \left[ n-1\right]$.   \medskip 

\textbf{(e)} If $n\geq 2$, then 

\[  \left(\text{\#  of }\sigma \in S_{n}\text{ with }\ell \left(\sigma \right) =2\right) = \frac{\left(n-2\right)\left(n+1\right)}{2}.  \]

 Indeed, the only permutations $\sigma \in S_{n}$ with $\ell \left( \sigma \right)=2$ are the products $s_{i}s_{j}$ with $1\leq i<j<n$ as well as the products $s_{i}s_{i-1}$ with $i\in \left\{ 2,3,\ldots ,n-1\right\} $. If $n\geq 2$, then there are $\frac{\left(n-2\right)\left(n+1\right)}{2}$ such products (and they are all distinct).   \medskip 

\textbf{(f)} For any $k\in \mathbb {Z}$, we have 

\[  \left(\text{\#  of }\sigma \in S_{n}\text{ with }\ell \left(\sigma \right) =k\right) = \left(\text{\#  of }\sigma \in S_{n}\text{ with }\ell \left( \sigma \right)=\binom {n}{2}-k\right).  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.binom.binom
def.binom.binom

For any numbers $n$ and $k$, we set

\begin{equation}  \binom {n}{k}=\begin{cases}  \frac{n\left( n-1\right) \left( n-2\right) \cdots \left( n-k+1\right) }{k!}, &  \text{if }k\in \mathbb {N};\\ 0, &  \text{else.}\end{cases} \end{equation}

 Note that “numbers” is to be understood fairly liberally here. In particular, $n$ can be any integer, rational, real or complex number (or, more generally, any element in a $\mathbb {Q}$-algebra), whereas $k$ can be anything (although the only nonzero values of $\binom {n}{k}$ will be achieved for $k\in \mathbb {N}$, by the above definition).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.invs
def.perm.invs

Let $n\in \mathbb {N}$ and $\sigma \in S_{n}$. \medskip 

\textbf{(a)} An \emph{inversion} of $\sigma $ means a pair $\left(i,j\right)$ of elements of $\left[n\right]$ such that $i<j$ and $\sigma \left(i\right) >\sigma \left(j\right)$. \medskip 

\textbf{(b)} The \emph{length} (also known as the \emph{Coxeter length}) of $\sigma $ is the \#  of inversions of $\sigma $. It is called $\ell \left( \sigma \right)$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.notations
def.perm.notations

Let $n \in \mathbb {N}$ and $\sigma \in S_n$. We introduce three notations for $\sigma $: 

\textbf{(a)} A \emph{two-line notation} of $\sigma $ means a $2 \times n$-array 

\[  \begin{pmatrix}  p_1 

&  p_2 

&  \cdots 

&  p_n 

\\ \sigma (p_1) 

&  \sigma (p_2) 

&  \cdots 

&  \sigma (p_n) 

\end{pmatrix},  \]

 where the entries $p_1, p_2, \ldots , p_n$ of the top row are the $n$ elements of $[n]$ in some order. Commonly, we pick $p_i = i$. 

\textbf{(b)} The \emph{one-line notation} (short, \emph{OLN}) of $\sigma $ means the $n$-tuple $(\sigma (1), \sigma (2), \ldots , \sigma (n))$. 

\textbf{(c)} The \emph{cycle digraph} of $\sigma $ is the directed graph with vertices $1, 2, \ldots , n$ and arcs $i \to \sigma (i)$ for all $i \in [n]$.

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
  "justification": "The blueprint fixes \u201cLet n \u2208 \u2115\u201d and, in part (f), \u201cFor any k \u2208 \u2124\u201d; the elaborated binders are exactly `\u2200 {n : \u2115} (k : \u2124)`. Its `Equiv.Perm (Fin n)` represents permutations of an ordered n-element set, matching `\u03c3 \u2208 S_n`. By the dependency bodies, `invCount \u03c3 = (inv \u03c3).card` and `inv \u03c3 = {p | p.1 < p.2 \u2227 \u03c3 p.1 > \u03c3 p.2}`, exactly the blueprint\u2019s definition of \u2113(\u03c3) as the number of inversions. The conclusion compares the cardinalities satisfying `\u2191(invCount \u03c3) = k` and `\u2191(invCount \u03c3) = \u2191(n.choose 2) - k`, matching the two counts with lengths `k` and `binom n 2 - k`. The casts to \u2124 correctly permit every integer k, including values outside the possible natural length range, and `Nat.choose n 2` agrees with the blueprint binomial coefficient for `n \u2208 \u2115` and lower argument 2."
}