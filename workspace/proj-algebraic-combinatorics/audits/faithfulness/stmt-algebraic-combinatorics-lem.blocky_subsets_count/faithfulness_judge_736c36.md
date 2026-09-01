## TARGET AlgebraicCombinatorics.SignedCounting.blocky_subsets_count (theorem) — ELABORATED SIGNATURE
∀ (d n k : ℕ),
  0 < d →
    (AlgebraicCombinatorics.SignedCounting.blockySubsets d n k).card =
      if k % d ≤ n % d then (n / d).choose (k / d) * (n % d).choose (k % d) else 0

Docstring: Blocky subsets correspond to choosing which complete blocks to include,
plus choosing elements from the partial block. The count depends on divisibility.

A blocky k-element subset S of [n] is uniquely determined by:
1. Which complete d-blocks are fully in S (a subset of {0, ..., n/d - 1} of size k/d)
2. Which elements of the partial block are in S (a subset of {0, ..., n%d - 1} of size k%d)

This gives a bijection with pairs from
  (Finset.range (n/d)).powersetCard (k/d) × (Finset.range (n%d)).powersetCard (k%d)
which has cardinality (n/d).choose(k/d) * (n%d).choose(k%d).

When k%d > n%d, no such subsets exist (can't choose k%d elements from n%d available). 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SignedCounting.blockySubsets (def)
ℕ → ℕ → ℕ → Finset (Finset ℕ)

Body:
fun d n k =>
  {S ∈ AlgebraicCombinatorics.SignedCounting.kSubsets n k | AlgebraicCombinatorics.SignedCounting.IsDBlocky d n S}

Docstring: The set of d-blocky k-element subsets of [n]. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SignedCounting.IsDBlocky (def)
ℕ → ℕ → Finset ℕ → Prop

Body:
fun d n S => S ⊆ Finset.range n ∧ ∀ i < n / d, (∀ j < d, i * d + j ∈ S) ∨ ∀ j < d, i * d + j ∉ S

Docstring: A subset S of [n] is d-blocky if for each complete d-block {id, id+1, ..., id+d-1}
contained in [n], the set S either contains all elements or none of the elements. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SignedCounting.decidableIsDBlocky (def)
(d n : ℕ) → (S : Finset ℕ) → Decidable (AlgebraicCombinatorics.SignedCounting.IsDBlocky d n S)

Body:
fun d n S => id inferInstance

## PROJECT DEPENDENCY AlgebraicCombinatorics.SignedCounting.kSubsets (def)
ℕ → ℕ → Finset (Finset ℕ)

Body:
fun n k => Finset.powersetCard k (Finset.range n)

Docstring: The set of k-element subsets of [n]. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

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

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF HMod.hMod
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMod α β γ] → α → β → γ

Docstring: `a % b` computes the remainder upon dividing `a` by `b`.
The meaning of this notation is type-dependent.
* For `Nat` and `Int` it satisfies `a % b + b * (a / b) = a`,
  and `a % 0` is defined to be `a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `%` in identifiers is `mod`.

## BASE-LIBRARY REF instHMod
{α : Type u_1} → [Mod α] → HMod α α α

## BASE-LIBRARY REF Nat.instMod
Mod ℕ

## BASE-LIBRARY REF Nat.decLe
(n m : ℕ) → Decidable (n ≤ m)

Docstring: A decision procedure for non-strict inequality of natural numbers, usually accessed via the
`DecidableLE Nat` instance.

Examples:
 * `(if 3 ≤ 4 then "yes" else "no") = "yes"`
 * `(if 6 ≤ 4 then "yes" else "no") = "no"`
 * `show 12 ≤ 12 by decide`
 * `show 5 ≤ 12 by decide`


## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF instMulNat
Mul ℕ

## BASE-LIBRARY REF Nat.choose
ℕ → ℕ → ℕ

Docstring: `choose n k` is the number of `k`-element subsets in an `n`-element set. Also known as binomial
coefficients. For the fact that this is the number of `k`-element-subsets of an `n`-element
set, see `Finset.card_powersetCard`. 

## BASE-LIBRARY REF HDiv.hDiv
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HDiv α β γ] → α → β → γ

Docstring: `a / b` computes the result of dividing `a` by `b`.
The meaning of this notation is type-dependent.
* For most types like `Nat`, `Int`, `Rat`, `Real`, `a / 0` is defined to be `0`.
* For `Nat`, `a / b` rounds downwards.
* For `Int`, `a / b` rounds downwards if `b` is positive or upwards if `b` is negative.
  It is implemented as `Int.ediv`, the unique function satisfying
  `a % b + b * (a / b) = a` and `0 ≤ a % b < natAbs b` for `b ≠ 0`.
  Other rounding conventions are available using the functions
  `Int.fdiv` (floor rounding) and `Int.tdiv` (truncation rounding).
* For `Float`, `a / 0` follows the IEEE 754 semantics for division,
  usually resulting in `inf` or `nan`. 

Conventions for notations in identifiers:

 * The recommended spelling of `/` in identifiers is `div`.

## BASE-LIBRARY REF instHDiv
{α : Type u_1} → [Div α] → HDiv α α α

## BASE-LIBRARY REF Nat.instDiv
Div ℕ

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

## BASE-LIBRARY REF HasSubset.Subset
{α : Type u} → [self : HasSubset α] → α → α → Prop

Docstring: Subset relation: `a ⊆ b`  

Conventions for notations in identifiers:

 * The recommended spelling of `⊆` in identifiers is `subset`.

## BASE-LIBRARY REF Finset.instHasSubset
{α : Type u_1} → HasSubset (Finset α)

## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Docstring: `range n` is the set of natural numbers less than `n`. 

## BASE-LIBRARY REF Or
Prop → Prop → Prop

Docstring: `Or a b`, or `a ∨ b`, is the disjunction of propositions. There are two
constructors for `Or`, called `Or.inl : a → a ∨ b` and `Or.inr : b → a ∨ b`,
and you can use `match` or `cases` to destruct an `Or` assumption into the
two cases.


Conventions for notations in identifiers:

 * The recommended spelling of `∨` in identifiers is `or`.

 * The recommended spelling of `\/` in identifiers is `or` (prefer `∨` over `\/`).

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Finset.instMembership
{α : Type u_1} → Membership α (Finset α)

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

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

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


## BASE-LIBRARY REF id
{α : Sort u} → α → α

Docstring: The identity function. `id` takes an implicit argument `α : Sort u`
(a type in any universe), and an argument `a : α`, and returns `a`.

Although this may look like a useless function, one application of the identity
function is to explicitly put a type on an expression. If `e` has type `T`,
and `T'` is definitionally equal to `T`, then `@id T' e` typechecks, and Lean
knows that this expression has type `T'` rather than `T`. This can make a
difference for typeclass inference, since `T` and `T'` may have different
typeclass instances on them. `show T' from e` is sugar for an `@id T' e`
expression.


## BASE-LIBRARY REF inferInstance
{α : Sort u} → [i : α] → α

Docstring: `inferInstance` synthesizes a value of any target type by typeclass
inference. This function has the same type signature as the identity
function, but the square brackets on the `[i : α]` argument means that it will
attempt to construct this argument by typeclass inference. (This will fail if
`α` is not a `class`.) Example:
```
#check (inferInstance : Inhabited Nat) -- Inhabited Nat

def foo : Inhabited (Nat × Nat) :=
  inferInstance

example : foo.default = (default, default) :=
  rfl
```


## BASE-LIBRARY REF instDecidableAnd
{p q : Prop} → [dp : Decidable p] → [dq : Decidable q] → Decidable (p ∧ q)

## BASE-LIBRARY REF Finset.instDecidableRelSubset
{α : Type u_1} → [DecidableEq α] → DecidableRel fun x1 x2 => x1 ⊆ x2

## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF Nat.decidableBallLT
(n : ℕ) →
  (P : (k : ℕ) → k < n → Prop) →
    [(n_1 : ℕ) → (h : n_1 < n) → Decidable (P n_1 h)] → Decidable (∀ (n_1 : ℕ) (h : n_1 < n), P n_1 h)

## BASE-LIBRARY REF instDecidableOr
{p q : Prop} → [dp : Decidable p] → [dq : Decidable q] → Decidable (p ∨ q)

## BASE-LIBRARY REF Finset.decidableMem
{α : Type u_1} → [_h : DecidableEq α] → (a : α) → (s : Finset α) → Decidable (a ∈ s)

## BASE-LIBRARY REF instDecidableNot
{p : Prop} → [dp : Decidable p] → Decidable ¬p

## BASE-LIBRARY REF Finset.powersetCard
{α : Type u_1} → ℕ → Finset α → Finset (Finset α)

Docstring: Given an integer `n` and a finset `s`, then `powersetCard n s` is the finset of subsets of `s`
of cardinality `n`. 

## INFORMAL STATEMENT
lem.blocky_subsets_count

\leanhelper  For $d > 0$, the number of $d$-blocky $k$-element subsets of $\{ 0, \ldots , n-1\} $ is 

\[  |\mathcal{B}(d, n, k)| = \begin{cases}  \binom {n/d}{k/d} \cdot \binom {n \bmod d}{k \bmod d}, &  \text{if } k \bmod d \leq n \bmod d; \\ 0, &  \text{otherwise.} \end{cases}  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.binom.binom
def.binom.binom

For any numbers $n$ and $k$, we set

\begin{equation}  \binom {n}{k}=\begin{cases}  \frac{n\left( n-1\right) \left( n-2\right) \cdots \left( n-k+1\right) }{k!}, &  \text{if }k\in \mathbb {N};\\ 0, &  \text{else.}\end{cases} \end{equation}

 Note that “numbers” is to be understood fairly liberally here. In particular, $n$ can be any integer, rational, real or complex number (or, more generally, any element in a $\mathbb {Q}$-algebra), whereas $k$ can be anything (although the only nonzero values of $\binom {n}{k}$ will be achieved for $k\in \mathbb {N}$, by the above definition).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.blockysubsets
def.blockySubsets

\leanhelper  The set of $d$-blocky $k$-element subsets of $\{ 0, \ldots , n-1\} $: 

\[  \mathcal{B}(d, n, k) := \bigl\{ S \in \binom {[n]}{k} : S \text{ is } d\text{-blocky}\bigr\} .  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.isdblocky
def.IsDBlocky

\leanhelper  A subset $S \subseteq \{ 0, \ldots , n-1\} $ is \emph{$d$-blocky} if $S \subseteq \{ 0, \ldots , n-1\} $ and for each block index $i \in \{ 0, \ldots , \lfloor n/d \rfloor - 1\} $, either all elements of $\{ id, id+1, \ldots , id+d-1\} $ are in $S$ or none are.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.ksubsets
def.kSubsets

\leanhelper  The set $\binom {[n]}{k}$ of $k$-element subsets of $\{ 0, \ldots , n-1\} $: 

\[  \binom {[n]}{k} := \bigl\{ S \subseteq \{ 0,\ldots ,n-1\}  : |S| = k\bigr\} .  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal binders `\u2200 (d n k : \u2115), 0 < d \u2192` match the blueprint\u2019s natural-number parameters and hypothesis \u201cFor d > 0.\u201d The counted object is exactly `(blockySubsets d n k).card`; by the dependency bodies this is the cardinality of `{S \u2208 kSubsets n k | IsDBlocky d n S}`, where `kSubsets n k = Finset.powersetCard k (Finset.range n)` and `IsDBlocky` requires each complete block indexed by `i < n / d` to be wholly included or wholly excluded. This agrees with the informal definitions. Finally, the conclusion `if k % d \u2264 n % d then (n / d).choose (k / d) * (n % d).choose (k % d) else 0` exactly matches the stated piecewise binomial formula."
}