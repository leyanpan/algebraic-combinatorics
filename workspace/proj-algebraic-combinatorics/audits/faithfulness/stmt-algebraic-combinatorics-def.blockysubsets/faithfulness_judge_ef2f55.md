## TARGET AlgebraicCombinatorics.SignedCounting.blockySubsets (def) — ELABORATED SIGNATURE
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

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

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
  "justification": "The target body filters exactly as the blueprint specifies: `{S \u2208 kSubsets n k | IsDBlocky d n S}` matches `\\{S \\in \\binom{[n]}k : S \\text{ is } d\\text{-blocky}\\}`. The dependency `kSubsets n k := Finset.powersetCard k (Finset.range n)` is precisely the finite set of cardinality-`k` subsets of `{0,\u2026,n-1}`. Likewise, `IsDBlocky` requires `S \u2286 Finset.range n` and, for every `i < n / d`, either `\u2200 j < d, i*d+j \u2208 S` or `\u2200 j < d, i*d+j \u2209 S`, exactly matching the informal block indices and all-or-none condition. The formal declaration accepts every `d : \u2115`; at `d = 0`, Lean's natural-number division convention merely gives a total extension beyond the ordinarily meaningful division-based wording and introduces no restrictive hypothesis."
}