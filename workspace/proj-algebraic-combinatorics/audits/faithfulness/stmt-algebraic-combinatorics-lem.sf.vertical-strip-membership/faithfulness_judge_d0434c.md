## TARGET SymmetricFunctions.mem_verticalNStripPartitions_iff (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} (mu : SymmetricFunctions.NPartition N) (n : ℕ) (lam : SymmetricFunctions.NPartition N),
  lam ∈ SymmetricFunctions.verticalNStripPartitions mu n ↔
    (∀ (i : Fin N), mu.parts i ≤ lam.parts i) ∧
      SymmetricFunctions.isVerticalStripFun lam.parts mu.parts ∧ SymmetricFunctions.hasSizeDiff mu.parts lam.parts n

Docstring: Complete characterization of membership in `verticalNStripPartitions`.

An N-partition λ is in `verticalNStripPartitions μ n` if and only if:
1. μ ⊆ λ (containment): μ_i ≤ λ_i for all i
2. λ/μ is a vertical strip: λ_i ≤ μ_i + 1 for all i
3. |λ| - |μ| = n (size constraint)

This characterization is useful for proving that specific partitions
belong to `verticalNStripPartitions μ n`. 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition (inductive)
ℕ → Type

Body:
SymmetricFunctions.NPartition.mk : {N : ℕ} → (parts : Fin N → ℕ) → (∀ (i j : Fin N), i ≤ j → parts j ≤ parts i) → SymmetricFunctions.NPartition N

Docstring: An N-partition is a list of length N with weakly decreasing nonnegative entries.
This corresponds to Definition def.sf.N-par in the source.

**Note:** This is `SymmetricFunctions.NPartition`, a local definition.
A canonical top-level `NPartition` exists in `NPartition.lean` with the same
semantics (using `antitone` as the field name instead of `weaklyDecreasing`).
See the section docstring for details. 

## PROJECT DEPENDENCY SymmetricFunctions.verticalNStripPartitions (def)
{N : ℕ} → SymmetricFunctions.NPartition N → ℕ → Finset (SymmetricFunctions.NPartition N)

Body:
fun {N} mu n =>
  Finset.image
    (fun x =>
      match x with
      | ⟨f, hf⟩ =>
        have hf' := ⋯;
        SymmetricFunctions.toNPartition f ⋯)
    {f ∈ SymmetricFunctions.potentialVerticalStrips mu |
        SymmetricFunctions.isWeaklyDecreasing f ∧
          SymmetricFunctions.isVerticalStripFun f mu.parts ∧ SymmetricFunctions.hasSizeDiff mu.parts f n}.attach

Docstring: The set of N-partitions λ such that λ/μ is a vertical n-strip.

This is the set of all N-partitions λ satisfying:
1. μ ⊆ λ (containment): μ_i ≤ λ_i for all i
2. Vertical strip: λ_i ≤ μ_i + 1 for all i
3. Size: |λ| - |μ| = n

The set is finite because each λ_i ∈ {μ_i, μ_i + 1}. 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.parts (def)
{N : ℕ} → SymmetricFunctions.NPartition N → Fin N → ℕ

Body:
fun N self => self.1

Docstring: The parts of the partition 

## PROJECT DEPENDENCY SymmetricFunctions.isVerticalStripFun (def)
{N : ℕ} → (Fin N → ℕ) → (Fin N → ℕ) → Prop

Body:
fun {N} lam mu => ∀ (i : Fin N), lam i ≤ mu i + 1

Docstring: A skew partition λ/μ is a vertical strip if no two boxes lie in the same row.
Equivalently: λ_i ≤ μ_i + 1 for all i.

The argument order `(lam, mu)` matches standard mathematical notation λ/μ.

**Related definitions:**
- `SkewPartition.isVerticalStrip`: Bundled version for `SkewPartition N` 

## PROJECT DEPENDENCY SymmetricFunctions.hasSizeDiff (def)
{N : ℕ} → (Fin N → ℕ) → (Fin N → ℕ) → ℕ → Prop

Body:
fun {N} mu lam n => ∑ i, lam i = ∑ i, mu i + n

Docstring: Check if |λ| - |μ| = n. 

## PROJECT DEPENDENCY SymmetricFunctions.isWeaklyDecreasing (def)
{N : ℕ} → (Fin N → ℕ) → Prop

Body:
fun {N} f => ∀ (i j : Fin N), i ≤ j → f j ≤ f i

Docstring: Check if a function forms a valid N-partition (weakly decreasing). 

## PROJECT DEPENDENCY SymmetricFunctions.instDecidableIsWeaklyDecreasing (def)
{N : ℕ} → (f : Fin N → ℕ) → Decidable (SymmetricFunctions.isWeaklyDecreasing f)

Body:
fun {N} f => Fintype.decidableForallFintype

## PROJECT DEPENDENCY SymmetricFunctions.instDecidableIsVerticalStripFun (def)
{N : ℕ} → (lam mu : Fin N → ℕ) → Decidable (SymmetricFunctions.isVerticalStripFun lam mu)

Body:
fun {N} lam mu => Fintype.decidableForallFintype

Docstring: Decidable instance for vertical strip predicate. 

## PROJECT DEPENDENCY SymmetricFunctions.instDecidableHasSizeDiff (def)
{N : ℕ} → (mu lam : Fin N → ℕ) → (n : ℕ) → Decidable (SymmetricFunctions.hasSizeDiff mu lam n)

Body:
fun {N} mu lam n => inferInstanceAs (Decidable (∑ i, lam i = ∑ i, mu i + n))

## PROJECT DEPENDENCY SymmetricFunctions.potentialVerticalStrips (def)
{N : ℕ} → SymmetricFunctions.NPartition N → Finset (Fin N → ℕ)

Body:
fun {N} mu => Fintype.piFinset fun i => Finset.Icc (mu.parts i) (SymmetricFunctions.verticalStripUpperBound mu i)

Docstring: A function from Fin N to ℕ that could potentially form a vertical n-strip with μ. 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.instDecidableEq (def)
{N : ℕ} → DecidableEq (SymmetricFunctions.NPartition N)

Body:
fun {N} lam mu => decidable_of_iff (lam.parts = mu.parts) ⋯

Docstring: Decidable equality for N-partitions. 

## PROJECT DEPENDENCY SymmetricFunctions.toNPartition (def)
{N : ℕ} → (f : Fin N → ℕ) → SymmetricFunctions.isWeaklyDecreasing f → SymmetricFunctions.NPartition N

Body:
fun {N} f hf => { parts := f, weaklyDecreasing := hf }

Docstring: Convert a valid function to an NPartition. 

## PROJECT DEPENDENCY SymmetricFunctions.verticalStripUpperBound (def)
{N : ℕ} → SymmetricFunctions.NPartition N → Fin N → ℕ

Body:
fun {N} mu i => mu.parts i + 1

Docstring: The bound for each λ_i when forming a vertical strip with μ.
λ_i must satisfy μ_i ≤ λ_i ≤ μ_i + 1 (vertical strip condition). 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.mk (constructor)
{N : ℕ} → (parts : Fin N → ℕ) → (∀ (i j : Fin N), i ≤ j → parts j ≤ parts i) → SymmetricFunctions.NPartition N

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Iff
Prop → Prop → Prop

Docstring: If and only if, or logical bi-implication. `a ↔ b` means that `a` implies `b` and vice versa.
By `propext`, this implies that `a` and `b` are equal and hence any expression involving `a`
is equivalent to the corresponding expression with `b` instead.


Conventions for notations in identifiers:

 * The recommended spelling of `↔` in identifiers is `iff`.

 * The recommended spelling of `<->` in identifiers is `iff` (prefer `↔` over `<->`).

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Finset.instMembership
{α : Type u_1} → Membership α (Finset α)

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF instLEFin
{n : ℕ} → LE (Fin n)

## BASE-LIBRARY REF Finset.image
{α : Type u_1} → {β : Type u_2} → [DecidableEq β] → (α → β) → Finset α → Finset β

Docstring: `image f s` is the forward image of `s` under `f`. 

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

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF instDecidableAnd
{p q : Prop} → [dp : Decidable p] → [dq : Decidable q] → Decidable (p ∧ q)

## BASE-LIBRARY REF Finset.attach
{α : Type u_1} → (s : Finset α) → Finset { x // x ∈ s }

Docstring: `attach s` takes the elements of `s` and forms a new set of elements of the subtype
`{x // x ∈ s}`. 

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

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

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


## BASE-LIBRARY REF Fintype.decidableForallFintype
{α : Type u_1} → {p : α → Prop} → [DecidablePred p] → [Fintype α] → Decidable (∀ (a : α), p a)

## BASE-LIBRARY REF Nat.decidableForallFin
{n : ℕ} → (P : Fin n → Prop) → [DecidablePred P] → Decidable (∀ (i : Fin n), P i)

## BASE-LIBRARY REF forall_prop_decidable
{p : Prop} → (P : p → Prop) → [Decidable p] → [(h : p) → Decidable (P h)] → Decidable (∀ (h : p), P h)

## BASE-LIBRARY REF Fin.decLe
{n : ℕ} → (a b : Fin n) → Decidable (a ≤ b)

## BASE-LIBRARY REF Nat.decLe
(n m : ℕ) → Decidable (n ≤ m)

Docstring: A decision procedure for non-strict inequality of natural numbers, usually accessed via the
`DecidableLE Nat` instance.

Examples:
 * `(if 3 ≤ 4 then "yes" else "no") = "yes"`
 * `(if 6 ≤ 4 then "yes" else "no") = "no"`
 * `show 12 ≤ 12 by decide`
 * `show 5 ≤ 12 by decide`


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


## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF Fintype.piFinset
{α : Type u_1} → [DecidableEq α] → [Fintype α] → {δ : α → Type u_4} → ((a : α) → Finset (δ a)) → Finset ((a : α) → δ a)

Docstring: Given for all `a : α` a finset `t a` of `δ a`, then one can define the
finset `Fintype.piFinset t` of all functions taking values in `t a` for all `a`. This is the
analogue of `Finset.pi` where the base finset is `univ` (but formally they are not the same, as
there is an additional condition `i ∈ Finset.univ` in the `Finset.pi` definition). 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Finset.Icc
{α : Type u_1} → [inst : Preorder α] → [LocallyFiniteOrder α] → α → α → Finset α

Docstring: The finset $[a, b]$ of elements `x` such that `a ≤ x` and `x ≤ b`. Basically `Set.Icc a b` as a
finset. 

## BASE-LIBRARY REF Nat.instPreorder
Preorder ℕ

## BASE-LIBRARY REF Nat.instLocallyFiniteOrder
LocallyFiniteOrder ℕ

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF decidable_of_iff
{b : Prop} → (a : Prop) → (a ↔ b) → [Decidable a] → Decidable b

Docstring: Transfer decidability of `a` to decidability of `b`, if the propositions are equivalent.
**Important**: this function should be used instead of `rw` on `Decidable b`, because the
kernel will get stuck reducing the usage of `propext` otherwise,
and `decide` will not work. 

## BASE-LIBRARY REF Fintype.decidablePiFintype
{α : Type u_5} → {β : α → Type u_4} → [(a : α) → DecidableEq (β a)] → [Fintype α] → DecidableEq ((a : α) → β a)

## INFORMAL STATEMENT
lem.sf.vertical-strip-membership

\leanhelper  An $N$-partition $\lambda $ belongs to $\mathrm{verticalNStripPartitions}(\mu , n)$ if and only if $\mu \subseteq \lambda $, $\lambda /\mu $ is a vertical strip, and $|\lambda | - |\mu | = n$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar
def.sf.Npar

An $N$\emph{-partition} will mean a weakly decreasing $N$-tuple of nonnegative integers. In other words, an $N$-partition means an $N$-tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{N}\right) \in \mathbb {N}^{N}$ with $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{N}$. 

The \emph{size} (or weight) of an $N$-partition $\lambda = (\lambda _1, \lambda _2, \ldots , \lambda _N)$ is defined to be $|\lambda | := \lambda _1 + \lambda _2 + \cdots + \lambda _N$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar-order
def.sf.Npar-order

\leanhelper  We define a partial order on $N$-partitions by componentwise comparison: $\mu \leq \nu $ iff $\mu _i \leq \nu _i$ for all $i \in [N]$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.par-subset
def.sf.par-subset

Let $\lambda $ and $\mu $ be two $N$-partitions. 

We say that $\mu \subseteq \lambda $ if and only if $Y\left( \mu \right) \subseteq Y\left( \lambda \right) $. Equivalently, $\mu \subseteq \lambda $ if and only if

\[  \text{each }i\in \left[ N\right] \text{ satisfies }\mu _{i}\leq \lambda _{i}.  \]

 Thus we have defined a partial order $\subseteq $ on the set of all $N$-partitions.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-diag
def.sf.skew-diag

Let $\lambda $ and $\mu $ be two $N$-partitions such that $\mu \subseteq \lambda $. Then, we define the \emph{skew Young diagram} $Y\left( \lambda /\mu \right) $ to be the set difference

\begin{align*}  Y\left( \lambda \right) \setminus Y\left( \mu \right) &  =\left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \left[ \lambda _{i}\right] \setminus \left[ \mu _{i}\right] \right\}  \\ &  =\left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \mathbb {Z}\text{ and }\mu _{i}<j\leq \lambda _{i}\right\}  . \end{align*}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.strips
def.sf.strips

Let $\lambda $ and $\mu $ be two $N$-partitions. 

\textbf{(a)} We write $\lambda /\mu $ for the pair $\left( \mu ,\lambda \right) $. Such a pair is called a \emph{skew partition}. 

\textbf{(b)} We say that $\lambda /\mu $ is a \emph{horizontal strip} if we have $\mu \subseteq \lambda $ and the Young diagram $Y\left( \lambda /\mu \right) $ has no two boxes lying in the same column. 

\textbf{(c)} We say that $\lambda /\mu $ is a \emph{vertical strip} if we have $\mu \subseteq \lambda $ and the Young diagram $Y\left( \lambda /\mu \right) $ has no two boxes lying in the same row. 

Now, let $n\in \mathbb {N}$. 

\textbf{(d)} We say that $\lambda /\mu $ is a \emph{horizontal }$n$\emph{-strip} if $\lambda /\mu $ is a horizontal strip and satisfies $\left\vert Y\left( \lambda /\mu \right) \right\vert =n$. 

\textbf{(e)} We say that $\lambda /\mu $ is a \emph{vertical }$n$\emph{-strip} if $\lambda /\mu $ is a vertical strip and satisfies $\left\vert Y\left( \lambda /\mu \right) \right\vert =n$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.vertical-n-strip-partitions
def.sf.vertical-n-strip-partitions

\leanhelper  The finite set of $N$-partitions $\lambda $ such that $\lambda /\mu $ is a vertical $n$-strip. This is computed by filtering all functions bounded by the vertical strip constraints.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ydiag
def.sf.ydiag

Let $\lambda $ be an $N$-partition. 

The \emph{Young diagram} of $\lambda $ is defined as the set

\[  \left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \left[ \lambda _{i}\right] \right\}  \subseteq \left\{  1,2,3,\ldots \right\}  ^{2}.  \]

 We visually represent each element $\left( i,j\right) $ of this Young diagram as a box in row $i$ and column $j$. 

We denote the Young diagram of $\lambda $ by $Y\left( \lambda \right) $.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target quantifies over exactly the intended data, `\u2200 {N : \u2115} (mu : ...NPartition N) (n : \u2115) (lam : ...NPartition N)`. Its three conjuncts match the blueprint: `(\u2200 (i : Fin N), mu.parts i \u2264 lam.parts i)` is precisely `\u03bc \u2286 \u03bb` by `def.sf.par-subset`; `isVerticalStripFun lam.parts mu.parts` unfolds to `\u2200 i, lam.parts i \u2264 mu.parts i + 1`, which together with containment says that each row gains at most one box, exactly the vertical-strip condition; and `hasSizeDiff mu.parts lam.parts n` unfolds to `\u2211 i, lam.parts i = \u2211 i, mu.parts i + n`. Under the preceding componentwise containment, this is equivalent to `|\u03bb| - |\u03bc| = n`. Finally, `verticalNStripPartitions` is built by filtering functions by the same lower bounds, upper bounds, weak decrease, and size equation, then converting them to `NPartition`s. Thus membership in the formal finset is equivalent to the blueprint\u2019s stated characterization."
}