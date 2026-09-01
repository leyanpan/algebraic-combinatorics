## TARGET AlgebraicCombinatorics.SubtractiveMethods.allEven_count_formula (theorem) — ELABORATED SIGNATURE
∀ (n d : ℕ),
  ↑(AlgebraicCombinatorics.SubtractiveMethods.allEvenTuples n d).card * 2 ^ d =
    ∑ k ∈ Finset.range (d + 1), ↑(d.choose k) * (↑d - 2 * ↑k) ^ n

Docstring: The main counting formula (Theorem `thm.cancel.all-even`):
The number of all-even n-tuples in `(Fin n → Fin d)` equals
`(1/2^d) ∑_{k=0}^d C(d,k) (d-2k)^n`.

This formula implies that `∑_{k=0}^d C(d,k) (d-2k)^n` is nonnegative
and divisible by `2^d`, which is not obvious from the formula itself
due to the alternating signs when `n` is odd.

Label: Theorem `thm.cancel.all-even` 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SubtractiveMethods.allEvenTuples (def)
(n d : ℕ) → Finset (Fin n → Fin d)

Body:
fun n d => Finset.filter AlgebraicCombinatorics.SubtractiveMethods.IsAllEven Finset.univ

Docstring: The set of all-even tuples in `(Fin n → Fin d)` 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SubtractiveMethods.IsAllEven (def)
{n d : ℕ} → (Fin n → Fin d) → Prop

Body:
fun {n d} x => ∀ (k : Fin d), Even {i | x i = k}.card

Docstring: An n-tuple `x : Fin n → Fin d` is "all-even" if each element of `Fin d`
occurs an even number of times. For example, the 4-tuple `(1,4,4,1)` is all-even
since 1 appears twice and 4 appears twice.

Label: Definition from Theorem `thm.cancel.all-even` 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SubtractiveMethods.instDecidableIsAllEven (def)
{n d : ℕ} → (x : Fin n → Fin d) → Decidable (AlgebraicCombinatorics.SubtractiveMethods.IsAllEven x)

Body:
fun {n d} x => inferInstanceAs (Decidable (∀ (k : Fin d), Even {i | x i = k}.card))

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


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

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF Int.instMul
Mul ℤ

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

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF HPow.hPow
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HPow α β γ] → α → β → γ

Docstring: `a ^ b` computes `a` to the power of `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `^` in identifiers is `pow`.

## BASE-LIBRARY REF instHPow
{α : Type u_1} → {β : Type u_2} → [Pow α β] → HPow α β α

## BASE-LIBRARY REF Monoid.toNatPow
{M : Type u_2} → [Monoid M] → Pow M ℕ

## BASE-LIBRARY REF Int.instMonoid
Monoid ℤ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Int.instAddCommMonoid
AddCommMonoid ℤ

## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Docstring: `range n` is the set of natural numbers less than `n`. 

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

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Nat.choose
ℕ → ℕ → ℕ

Docstring: `choose n k` is the number of `k`-element subsets in an `n`-element set. Also known as binomial
coefficients. For the fact that this is the number of `k`-element-subsets of an `n`-element
set, see `Finset.card_powersetCard`. 

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

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Pi.instFintype
{α : Type u_3} →
  {β : α → Type u_4} → [DecidableEq α] → [Fintype α] → [(a : α) → Fintype (β a)] → Fintype ((a : α) → β a)

Docstring: A dependent product of fintypes, indexed by a fintype, is a fintype. 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Even
{α : Type u_2} → [Add α] → α → Prop

Docstring: An element `a` of a type `α` with addition satisfies `Even a` if `a = r + r`,
for some `r : α`. 

## BASE-LIBRARY REF Decidable
Prop → Type

Docstring: Either a proof that `p` is true or a proof that `p` is false. This is equivalent to a `Bool` paired
with a proof that the `Bool` is `true` if and only if `p` is true.

`Decidable` instances are primarily used via `if`-expressions and the tactic `decide`. In
conditional expressions, the `Decidable` instance for the proposition is used to select a branch. At
run time, this case distinction code is identical to that which would be generated for a
`Bool`-based conditional. In proofs, the tactic `decide` synthesizes an instance of `Decidable p`,
attempts to reduce it to `isTrue h`, and then succeeds with the proof `h` if it can.

Because `Decidable` carries data, when writing `@[simp]` lemmas which include a `Decidable` instance
on the LHS, it is best to use `{_ : Decidable p}` rather than `[Decidable p]` so that non-canonical
instances can be found via unification rather than instance synthesis.


## BASE-LIBRARY REF inferInstanceAs
(α : Sort u) → [i : α] → α

Docstring: `inferInstanceAs α` synthesizes a value of any target type by typeclass
inference. This is just like `inferInstance` except that `α` is given
explicitly instead of being inferred from the target type. It is especially
useful when the target type is some `α'` which is definitionally equal to `α`,
but the instance we are looking for is only registered for `α` (because
typeclass search does not unfold most definitions, but definitional equality
does.) Example:
```
#check inferInstanceAs (Inhabited Nat) -- Inhabited Nat
```


## BASE-LIBRARY REF Nat.decidableForallFin
{n : ℕ} → (P : Fin n → Prop) → [DecidablePred P] → Decidable (∀ (i : Fin n), P i)

## BASE-LIBRARY REF Nat.instDecidablePredEven
DecidablePred Even

## INFORMAL STATEMENT
thm.cancel.all-even

Let $n\in \mathbb {N}$ and $d\in \mathbb {N}$. Then, the number of all all-even $n$-tuples $\left( x_{1},x_{2},\ldots ,x_{n}\right) \in \left[ d\right] ^{n}$ is 

\[  \frac{1}{2^{d}}\sum _{k=0}^{d}\binom {d}{k}\left( d-2k\right) ^{n}.  \]

 More precisely (avoiding division), the number of all-even $n$-tuples multiplied by $2^d$ equals $\sum _{k=0}^{d}\binom {d}{k}(d-2k)^n$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.binom.binom
def.binom.binom

For any numbers $n$ and $k$, we set

\begin{equation}  \binom {n}{k}=\begin{cases}  \frac{n\left( n-1\right) \left( n-2\right) \cdots \left( n-k+1\right) }{k!}, &  \text{if }k\in \mathbb {N};\\ 0, &  \text{else.}\end{cases} \end{equation}

 Note that “numbers” is to be understood fairly liberally here. In particular, $n$ can be any integer, rational, real or complex number (or, more generally, any element in a $\mathbb {Q}$-algebra), whereas $k$ can be anything (although the only nonzero values of $\binom {n}{k}$ will be achieved for $k\in \mathbb {N}$, by the above definition).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.cancel.all-even
def.cancel.all-even

\leanhelper  Let $n\in \mathbb {N}$ and $d\in \mathbb {N}$. An $n$-tuple $\left( x_{1},x_{2},\ldots ,x_{n}\right) \in \left[ d\right] ^{n}$ is said to be \emph{all-even} if each element of $\left[ d\right] $ occurs an even number of times in this $n$-tuple (i.e., if for each $k\in \left[ d\right] $, the number of all $i\in \left[ n\right] $ satisfying $x_{i}=k$ is even).

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
  "justification": "The target quantifies exactly as required: `\u2200 (n d : \u2115)`. By `allEvenTuples n d = Finset.filter IsAllEven Finset.univ`, its cardinal counts functions `Fin n \u2192 Fin d`, the finite-type counterpart of tuples in `[d]^n`. The predicate `IsAllEven x = \u2200 (k : Fin d), Even {i | x i = k}.card` exactly matches the informal condition that every value occurs an even number of times. The equality `\u2191(allEvenTuples n d).card * 2 ^ d = \u2211 k \u2208 Finset.range (d + 1), \u2191(d.choose k) * (\u2191d - 2 * \u2191k) ^ n` is an equality in `\u2124`, so `(d-2k)^n` uses signed integer subtraction rather than truncated natural subtraction. `Finset.range (d + 1)` indexes precisely `k = 0,\u2026,d`, and `Nat.choose d k` agrees with the stated binomial coefficient for these natural arguments. Thus the formal equality is exactly the informal division-free formula."
}